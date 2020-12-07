# 移动页面禁用body滚动

### 场景：

有一个移动页面，默认情况下是可以滚动的，
然后打开弹窗，发现滑动的时候，主body还是会跟着滚动
所以就需要当找开弹窗的时候，先临时禁用body的滚动


### 1. 定义控制body不能滚动的样式类
```css
body.noscroll {
	position: fixed;
	overflow: hidden;
	top:0;
	bottom:0;
	left:0;
	right:0;
}
```

### 2. 用js在弹窗/关闭弹窗的时候对body进行样式控制
```javascript
$("btn.openwin").on("click", function(){
	$("body").addClass("noscroll");
});

$("btn.closewin).on("click", function(){
	$("body").removeClass("noscroll");
});
```