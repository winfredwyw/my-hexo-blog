---
title: JS-FontSize文字大小适配方案
date: 2017-07-05 15:57:08
tags: javascript,适配

---
## 背景

目前移动wap最成熟的rem适配方式，在安卓部分机型上适配文字大小时，由于换算成rem单位后，安卓系统里面的浏览器对该rem值的小数位处理机制不一致（有的会四舍五入，而有的可能只保留整数等等），会导致安卓系统下文字大小与设计稿存在偏差的明显缺陷。本文针对上述缺陷提出了一种通过JS-FontSize适配文字大小的解决方案。

## 思路

* 1、该方法就是js渲染模版之前，通过js计算屏幕宽度与设计稿宽度之比（用于后面步骤2适配文字换算）
* 2、循环12~44之间偶数文字大小（包括12和44，选择这个大小区间，是因为基本可以覆盖设计稿文字大小范围），乘以步骤1里面拿到的比，获得适配当前屏宽的对应字体大小对象，格式示例：{key:value,key:value...}
* 3、在编写模版的时候，直接用约定好的key值（推荐key值为：fs + 设计稿文字大小，比如28，这里key就是：fs28）取步骤2里面得到的对象里面的value值，设置行内样式，以实现文字大小适配

## 适用条件

* 1、js渲染模版
* 2、移动wap

## 细节

### 1、js渲染之前，计算好12~44换算后对应的文字大小
```
// 文字大小适配对象
const G_FONTSIZE_STYLES = (function () {
    // 屏幕宽度
    let WIN_WIDTH = document.body.clientWidth;
    // 设计稿宽度
    let UI_WiDTH = 750;

    let result = {};

    // 获取屏幕与设计稿的宽度比
    let getFitVal = function () {
        let val = WIN_WIDTH / UI_WiDTH;
        return val.toFixed(2);
    };

    // 字体大小自适应
    let getFitFontSize = function (fs) {
        if (!Util.isString(fs))
            return '0px';
        let fsNum = parseInt(fs.replace(/px/g, ''), 10);
        let fitVal = getFitVal();
        let fitFsNum = fsNum * fitVal;

        return fitFsNum.toFixed(0) + 'px';
    };

    // 生成文字大小样式对象集合
    let mapFitFontSize = function () {
        let fsArr = [12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44];

        fsArr.map(function (item) {
            let key = 'fs' + item;
            let val = getFitFontSize(item + 'px');

            result[key] = {
                fontSize: val
            };
        });
    };
    mapFitFontSize();

    return result;

})();
```
### 2、渲染的时候,在模版上写入对应的文字style

```
    style={G_FONTSIZE_STYLES.fs28}
```
