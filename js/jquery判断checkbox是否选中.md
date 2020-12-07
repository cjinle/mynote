# jquery判断checkbox是否选中

```javascript
/* 所有的checkbox为选中 */
$("input[type='checkbox']").attr("checked", true);


/* 所有的checkbox不选中 */
$("input[type='checkbox']").attr("checked", false);
$("input[type='checkbox']").removeAttr("checked");

/* 判断checkbox是否为选中 */
var cboxObj = $("input[type='checkbox']"); // checkbox的对象
if (cboxObj.is(":checked")) { 
// 这里为选中状态
} else {
// 这里为没选中状态
}
```

