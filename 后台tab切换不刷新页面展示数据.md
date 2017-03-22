html:

```
<ul>
	<li><a href="/contract/coursedetail/list.json?contractId=${obj.contract.id }" class="j-ajax" rel="courseDetail"><span>课程明细</span></a></li>
</ul>
```
java
```
/**
	 * 保存
	 * 
	 * @param CourseDetailAddForm 课程明细添加表单
	 */
	@At
	public Object save(@Param("..") final CourseDetailAddForm courseDetailAddForm) {
		courseDetailViewService.save(courseDetailAddForm);
		return JsonResult.success("保存成功", "courseDetail", false);
	}
```

> 以上代码防止刷新真个tab列表


dialog 提交form表单 回调

<form action="/contract/coursedetail/save.json" method="post" class="pageForm required-validate" onsubmit="return validateCallback(this, objectDetailed);">


function objectDetailed(data){
	navTabAjaxDone(data);//必须;	
	$('.tabsHeaderContent li.selected a').click();
}
