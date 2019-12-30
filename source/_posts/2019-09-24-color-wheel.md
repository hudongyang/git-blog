---
title: 色轮的canvas实现
date: 2019-09-24 18:23:44
tags:
---

效果见[这儿](http://static.hudongyang.cn/color-wheel/color-wheel.html)

### 基础知识
#### 色轮（Color Wheel）
典型的 macOS 下的色轮如下图：

![](http://static.hudongyang.cn/images/1569307825816.png)
色轮是用来研究色彩关系的工具，也是设计时颜色选择的工具。比如我们在 pages 中更改某些文字的颜色。

#### 色彩模型（Color Mode）
常用的色彩模型有四种：CMYK、RGB、HEX和HSB。
比如红色分别表示为：
- RGB:      255, 0, 0
- CMYK:   0, 100, 0, 0
- HEX:       FF0000
- HSB:       0, 100, 50  

下面解释一下本文用到的 RGB 和 HSB 两种色彩模型
##### RGB
RGB 表示Red（红色）、Green（绿色）和Blue（蓝色）。我们的电脑、手机等电子设备上的颜色就是用RGB表示。所有颜色都由这三种组合而成。要在电子设备上显示其它模型的颜色，需要将其它模型转化为RGB（本文即是这样）。
##### HSB
HSB 又叫 HSV，表示 Hue（色相）、Saturation（饱和度）、Brightness（亮度）。色相将色轮分割为**三百六十度**，所以通过色相就能够初步判定大概的颜色；饱和度越高颜色越鲜艳，越低则接近无色（黑、白、灰）；亮度越低就越接近黑色。  
![](http://static.hudongyang.cn/images/1569311111373.png)
由上图可见，HSB的色彩模型和色轮很像，我们便是基于它进行色轮的绘制。
HSB 完全符合人们对色彩理解的直觉，稍加熟悉，甚至能通过直接看 HSB 代码猜出其表达的颜色来。而且 HSB 非常适合「组调色方案时，不想变换亮度以及饱和度」的情况，你只需要调整 hue（色相），便能得出一个和上一个颜色不同却又十分统一的新颜色。  
![](http://static.hudongyang.cn/images/1569310698454.png "只改变色相即可得到风格统一的不同颜色")

### 代码实现
我们的目标是在一个 100 x 100 像素的正方形中画出一个圆形的色轮。

#### 创建 imageData 
首先创建一个 100 x 100 像素 画布
```html
<canvas width="100" height="100"></canvas>
```

再创建一个 ImageData 对象
```javascript
const canvas = document.querySelector('canvas') as HTMLCanvasElement
const ctx = canvas.getContext('2d')
const imageData = ctx.createImageData(100, 100)
```

ImageData 对象中存储着 canvas 对象真实的像素数据，它包含以下几个只读属性：
- **width** 图片宽度，单位是像素
- **height** 图片高度，单位是像素
- **data** Uint8ClampedArray 类型的一维数组，包含着RGBA格式的整型数据，范围在0至255之间（包括255）。  

关于 canvas 中的像素操作，详见 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial/Pixel_manipulation_with_canvas)。  

对于一个 100 x 100 像素的画布来说，共有 100 \* 100 = 10000 个像素点。另每个像素点用 RGBA 4位表示，由此推算出 data 数组的长度为：10000 \* 4 = 40000。因此，我们的目标转化为计算画布中每个像素的 RGBA 值，并回填入 data 中。

#### 遍历像素
以中心点为原点（0，0）建立坐标系，遍历 canvas 的的像素，获得每个像素的坐标。
```ts
const radius = imageData.width / 2
for (let x = -radius; x < radius; x++) {
    for (let y = -radius; y < radius; y++) {
        // (x, y) 即为每个像素的坐标
    }
}
```

#### 角度和距离的计算
我们再次观察一下 HSB 颜色模型的示意图：  

![](http://static.hudongyang.cn/images/1569311111373.png)
先不考虑纵向的明亮度，HSB 模型的色相与角度相关，饱和度与到原点的距离相关。因此可以说，HSB 模型的颜色可以由该颜色的角度和到原点的距离决定。咱们便是利用这一点来实现咱们的色轮。
回到色轮，我们基于 HSB 模型来绘制色轮，需要知道色轮中每个像素点的角度和到原点的距离。但是，目前我们只知道每个像素点的x、y坐标。因此，要基于(x, y) 坐标，来计算角度和距离。如下图所示：  

![](http://static.hudongyang.cn/images/1569317782248.png)

对于距离 r ，利用勾股定理即可
```ts
let r = Math.sqrt(x * x + y * y)
```

对于角度 𝜃 ，利用三角函数 
```bash
tan𝜃 = y / x
```

代码为：
```ts
let phi = Math.atan2(y, x)
```

完整的代码：
```ts
function xy2polar(x, y) {
    let r = Math.sqrt(x * x + y * y);
    let phi = Math.atan2(y, x);
    return [r, phi];
}

const radius = imageData.width / 2
for (let x = -radius; x < radius; x++) {
    for (let y = -radius; y < radius; y++) {
        const [r, phi] = xy2polar(x, y)
        // r 即为距离，phi 为角度
    }
}
```

此处的角度单位为**弧度**，还需要转化为**度**。
```ts
function rad2deg(rad) {
    return (rad + Math.PI) / (2 * Math.PI) * 360;
}
```

转换后的角度值即是 HSV 中的 H 值。距离与半径的比值即为 S 值。V 值暂时可以给个默认值 1。

#### 最终实现
知道了 HSV的值是不是就可以了呢？答案是否定的。还有几个问题需要解决。

- 由于色轮是圆形，因此要排除那些距离大于半径的像素点
```ts
const [r, phi] = xy2polar(x, y)

if (r > radius) {
    continue
}
```

- 我们知道了 HSV 的值，但是 ImageData 中需要的是 RGB 的值，因此需要转换，转换函数为：
```ts
function hsv2rgb(hsv: HSV): RGB {
    let chroma = hsv.value * hsv.saturation;
    let hue1 = hsv.hue / 60;
    let x = chroma * (1 - Math.abs((hue1 % 2) - 1));
    let r1, g1, b1;

    if (hue1 >= 0 && hue1 <= 1) {
        ([r1, g1, b1] = [chroma, x, 0]);
    } else if (hue1 >= 1 && hue1 <= 2) {
        ([r1, g1, b1] = [x, chroma, 0]);
    } else if (hue1 >= 2 && hue1 <= 3) {
        ([r1, g1, b1] = [0, chroma, x]);
    } else if (hue1 >= 3 && hue1 <= 4) {
        ([r1, g1, b1] = [0, x, chroma]);
    } else if (hue1 >= 4 && hue1 <= 5) {
        ([r1, g1, b1] = [x, 0, chroma]);
    } else if (hue1 >= 5 && hue1 <= 6) {
        ([r1, g1, b1] = [chroma, 0, x]);
    }

    let m = hsv.value - chroma;
    let [r, g, b] = [r1 + m, g1 + m, b1 + m];

    return {
        red: 255 * r,
        green: 255 * g,
        blue: 255 * b,
        alpha: hsv.alpha
    }
} 
```

- 最后，还需计算每个像素点对应 ImageData 中的data 数组的索引。注意 data 数组是按照从左到右、从上到下的顺序存储像素的 RGBA 数据的。
```ts
const index = ((x + radius) * imageData.width + (y + radius)) * 4
```

完整的代码：
```ts
const radius = image.width / 2
for (let x = -radius; x < radius; x++) {
    for (let y = -radius; y < radius; y++) {
        const [r, phi] = xy2polar(x, y)

        if (r > radius) {
            continue
        }

        const index = ((x + radius) * image.width + (y + radius)) * 4

        const deg = rad2deg(phi)
        const rgb = hsv2rgb({hue: deg, saturation: r / radius, value: 1.0, alpha: 255})

        image.data[index] = rgb.red
        image.data[index + 1] = rgb.green
        image.data[index + 2] = rgb.blue
        image.data[index + 3] = rgb.alpha
    }
}
```

调用 `ctx.putImageData(image, 0, 0)` 即完成绘制。

完整的代码在 [github](https://github.com/hudongyang/color-wheel)