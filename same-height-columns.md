### CSS 多列等高

1. 优良方法，display:table-row 结合 display:table-cell(IE6/7不支持)
2. 退化方法：每一列都利用：padding-bottom + margin-bottom 互相抵消(绝对值需要足够高)；同时父容器overflow：hidden，隐藏多余内容
