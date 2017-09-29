### CSS 多列等高

1. 优良方法，display:table-row 结合 display:table-cell(IE6/7不支持)
2. 退化方法：每一列都利用：padding-bottom + margin-bottom 互相抵消(绝对值需要足够高)；同时父容器overflow：hidden，隐藏多余内容

### 高度与宽度成比例效果

1. 需求：元素在跟随父元素大小变化时候保持固定宽高比；假设高度 100px，宽度 200px
2. 传统 height:auto 这种方式问题：图片加载出来之前布局被影响；假如有列表，图片容不得1px的差异
3. 父元素样式：

```css
.container{
  padding-bottom: 50%; //即 100/200 * 100%
  height: 0;
  overflow: hidden;//optional clear-fix
}
.container::after{//optional clear-fix
  display: block;
  content: '';
  height: 0;
  visibility: hidden;
  clear: both;
}
.inner{
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;//比例保证了width
}
```
{ padding-bottom: 子元素宽/子元素高 * 100%;height:0;/*overflow:hidden;*/}, &::after{display:block;content:'';height:0;clear:both;}
4. 子元素样式：{ width:100%;float:left; }
4. 更深层次应用还可根据元素大小变化区间设置宽高比(斜率为padding-bottom)，达到某些适应效果
5. 父容器使用 `overflow:hidden` 在包含图片、iframe、video 等没有问题；如果是文本，并且内容多出高度，则 overflow 会截取文本内容 
6. **参考资料**[aspect-ratio-boxes](https://www.w3cplus.com/css/aspect-ratio-boxes.html)
7. iOS 设备设置了 meta\[viewport] 的时候，html 及 body 的 overflow hidden 会被忽略，故宜再包一层的div
8. line-height 属性默认为1.2左右，因 font-family 而异，比如font-size:28px, 单行 content-box 高度约为 33px
9. 多栏等高：padding-bottom: 5000px(much bigger) 结合 margin-bottom: 5000px(容器搭配 overflow:hidden 防止padding背景色污染其他页面内容)
10. 多栏等高：人造栏（实际是容器背景结合元素自身背景覆盖）可以实现多栏等高效果（模拟）
