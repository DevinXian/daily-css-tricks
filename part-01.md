### CSS 多列等高

1. 优良方法，display:table-row 结合 display:table-cell(IE6/7不支持)
2. 退化方法：每一列都利用：padding-bottom + margin-bottom 互相抵消(绝对值需要足够高)；同时父容器overflow：hidden，隐藏多余内容

### 高度与宽度成比例效果

1. 需求：元素在跟随父元素大小变化时候保持固定宽高比；假设高度 100px，宽度 200px
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
.dist{
  width:100%;
  float: left;
}
```
{ padding-bottom: 子元素宽/子元素高 * 100%;height:0;/*overflow:hidden;*/}, &::after{display:block;content:'';height:0;clear:both;}
4. 子元素样式：{ width:100%;float:left; }
4. 更深层次应用还可根据元素大小变化区间设置宽高比(斜率为padding-bottom)，达到某些适应效果
