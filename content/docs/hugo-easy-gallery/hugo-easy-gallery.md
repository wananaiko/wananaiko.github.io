---
title: "Hugo增加相册功能"
date: 2023-01-12T22:54:52+08:00
author: "wananaiko"
tags:
  - Hugo
  - 相册
---

相册效果如下：

{{< load-photoswipe >}}
{{< gallery >}}
  {{< figure src="https://images.wananaiko.com/2023/01/jaeYun.jpg" alt="法师桥">}}
  {{< figure src="https://images.wananaiko.com/2023/01/OuL560.jpg" alt="龙美术馆" >}}
  {{< figure src="https://images.wananaiko.com/2023/01/4cxcoH.jpg" alt="拍摄于前滩太古里，使用了 Leica M10 + 50 2aa">}}
{{< /gallery >}}



Github仓库地址:
https://github.com/liwenyip/hugo-easy-gallery

按教程操作后,需要注意在文章中引用时,按下面的类似格式 (需去掉下方所有的 \ ):

```markdown
{{\< load-photoswipe >}}
{{\< gallery >}}
  {{\< figure link="docs/hugo-easy-gallery/image1.jpg" >}}
  {{\< figure link="docs/hugo-easy-gallery/image2.jpg" >}}
  {{\< figure link="docs/hugo-easy-gallery/image3.jpg" >}}
{{\< /gallery >}}
```
并对 CSS 样式进行了微调,修改根目录 `/assets/css/core/reset.css`,加入以下代码:
```css
/* 相册弹窗中的样式调整 */
.gallery {
    overflow: hidden;
    margin: 0 auto !important;
    max-width: 790px !important;
}

.pswp__item {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    overflow: hidden;
    background-color: #000000 !important;
}

.pswp img {
    max-width: none;
    /* max-height: 85vh; */
}

.pswp__caption {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    min-height: 72px !important;
}

.pswp__counter {
    position: absolute;
    left: 10px;
    top: 0;
    height: 44px;
    font-size: 13px;
    line-height: 44px;
    color: #FFF;
    opacity: .75;
    padding: 0 20px;
}

.pswp__caption__center {
    text-align: left;
    max-width: 790px !important;
    margin: 0 auto !important;
    font-size: 13px;
    padding: 10px;
    line-height: 20px;
    color: #CCC;
}

.esc_window {
    float: left;
    height: 44px;
    font-size: 13px;
    line-height: 44px;
    color: #fff;
    opacity: .75;
    padding: 0 10px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.icon_right {
    padding-right: 10px;
}

.pswp__ui--fit .pswp__top-bar, .pswp__ui--fit .pswp__caption {
    background-color: rgba(0,0,0) !important;
}
```



修改了 `/themes/PaperModX/layouts/shortcodes/load-photoswipe.html`，在`<div class="pswp__counter"></div>`这行代码下面加了一行按 ESC 关闭窗口的提示文字，对应的样式在上面写了。

```html
<div class="esc_window">按ESC关闭窗口</div>
```



并使用 `<div class="icon_right">` 包裹了右侧的4个图标。

```html
<div class="icon_right">
   <button class="pswp__button pswp__button--close" title="Close (Esc)"></button>
   <button class="pswp__button pswp__button--share" title="Share"></button>
   <button class="pswp__button pswp__button--fs" title="Toggle fullscreen"></button>
   <button class="pswp__button pswp__button--zoom" title="Zoom in/out"></button>
</div>
```