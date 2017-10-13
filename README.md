# Dropdown
Dropdown是面向PC端的基于jQuery开发的轻量级下拉框插件，支持key/value搜索，有token和select两种模式。

## Version
- 1.2.0

## Support
- Internet Explorer 8+
- Chrome for PC
- Safari for PC
- Firefox for  PC

## Based
- jQuery 1.4+

## Log
* 2017-10-13 version 1.2.0
	* 新增方法 `reset`
	* 搜索支持分组名
* 2017-08-05 version 1.1.7
  * 修复BUG [#6](/../../issues/8)

* 2017-08-05 version 1.1.6
  * 新增自定义字段 `extendProps`
  * 新增方法 `choose`
  * 优化回调函数 `choice(event,data)`，新增第二个入参
  * [#6](/../../issues/6)
* 2017-07-19 version 1.1.5
  * 新增 `init` 回调函数
  * 修复 [#4](/../../issues/4) 的问题
* 2017-07-06 version 1.1.4
  * 修复`value`值为中文时的错误 [#2](/../../issues/2)
  * 修复单选无法触发回调问题 [#2](/../../issues/2)
  * 修复`destroy`时，事件未被移除的BUG [#3](/../../issues/3)
* 2017-07-03 version 1.1.3
  * 新增 `update` 方法
  * 修复 `点击清除按钮默认提交表单` 的行为。
* 2017-06-28 version 1.1.1
  * 修复 `IE8` 不兼容的问题

* 2017-06-24 version 1.1.0
	* 多选 `select`模式下增加一个 **全部删除** 按钮
	* 新增 `changeStatus` 方法，提供`readonly`,`disabled`功能
	* 新增 `destroy`,`bindEvent`,`unbindEvent` 方法
* 2017-06-21 version 1.0.0 上线


## Feature
1. 支持 `select` 和 `token` 两种模式
2. 支持 `optgroup` 分组
3. 保留原生 `select` 的键盘操作
4. 数据源可以直接通过接口 `data` 注入，也可以直接渲染 `select>option` ，由插件自动转换。
5. 插件同步 `select` 和 `ul>li` 标签，便于表单字段提交及前端校验，

## Principle
**程序设计原理如下图所示：**
![](http://images.vrm.cn/2017/03/21/WX20170321-174303.png)

在一些前端渲染的场景，JSON数据是通过AJAX请求的，如果再拼成`<option value="yyy">xxx</option>` 就有点多余了。
在这种情况下，建议直接将JSON数据转为以下这种格式：

```json
[
    {
      "id": 1, // value值
      "disabled": false, // 是否禁选
      "groupName": "分组名",  
      "groupId": 3,//分组ID
      "selected": false, // 是否选中
      "name": "Betty Deborah Jackson" // 名称
    },
    {
      "id": 2,
      "disabled": false,
      "groupName": "分组名",
      "groupId": 2,
      "selected": false,
      "name": "Jason Barbara Clark"
    }
    // more ...
    ]
```

Dropdown 会根据这个JSON来渲染 `select > option`

## Options
| 名称 | 描述 | 类型|默认|
| ----|-----|-----|----|
| readOnly|是否只读|Boolean|`false`|
|limitCount|选择上限|Number|`Infinity`|
| input|搜索框模板|HTML|`<input type="text" maxLength="20" placeholder="搜索关键词或ID">`|
| data|数据源|Array|`[]`|
| searchable|是否可开启搜索|Boolean|`true`|
| searchNoData|无数据模板|HTML|`<li style="color:#ddd">查无数据，换个词儿试试 /(ㄒoㄒ)/~~</li>`|
| choice|选择后回调函数|Function| `function(){}`|
| init|插件初始化后回调函数|Function| `function(){}`|
| extendProps|扩展自定义字段 `data-*`,字段名必须在`data`中存在，否则无效 **不建议扩展太多字段，会有性能影响**|Array| `['prop1','prop2']`|

## Methods

### changeStatus(status)
修改组件状态

| 参数 |类型|描述|
| ----|-----|-----|
| status|String|支持`readonly`或`disabled`，不传则取消`readonly/disabled`|
|return|undefined|


```js
var dropdown = $('selector').dropdown(options).data('dropdown');
dropdown.changeStatus('readonly') // readonly
dropdown.changeStatus('disabled') // disabled
dropdown.changeStatus() // cancel

```
### choose(value,status)
动态选择值

| 参数 |类型|描述|
| ----|-----|-----|
| value | String\|Array | 需要被选中的值，多个值用数字 `['one','two','three']`
| status|Boolean|选中或取消，默认为: true
|return|undefined|


```js
var dropdown = $('selector').dropdown(options).data('dropdown');
dropdown.destroy();

```

### update(Array,isCover)
更新数据

| 参数 |类型|描述|
| ----|-----|-----|
| data|Array|需要更新的数据|
| isCover|Boolean|是否覆盖原有数据，默认不覆盖|


### destroy()
销毁组件

| 参数 |类型|描述|
| ----|-----|-----|
|return|undefined|

<!-- | status|String|支持`readonly`或`disabled`，不传则取消`readonly/disabled`| -->

```js
var dropdown = $('selector').dropdown(options).data('dropdown');
dropdown.destroy();

```


### reset()
重置

| 参数 |类型|描述|
| ----|-----|-----|
|return|undefined|


```js
var dropdown = $('selector').dropdown(options).data('dropdown');
dropdown.reset();

```

## Usage
引入

```html
<script src="http://cdn.bootcss.com/jquery/1.8.1/jquery.js"></script>
<link rel="stylesheet" type="text/css" href="./jquery.dropdown.css">
<script src="./jquery.dropdown.js"></script>
```

HTML 部分

```html
<div class="dropdown-mul-1">
   <!-- PS: select标签需手动设置隐藏 -->
	<select style="display:none"  name="" id="" multiple placeholder="请选择">
	    <option value="1">1</option>
	    <option value="2">2</option>
	    <option value="3">3</option>
	    <option value="4">4</option>
	    <option value="5">5</option>
	    <option value="6">6</option>
	    <option value="7">7</option>
	    <option value="8">8</option>
	    <option value="9">9</option>
	    <option value="10">10</option>
	    <option value="11">11</option>
	    <option value="12">12</option>
	</select>
</div>
```
JavaScript 部分

```js
$('.dropdown-mul-1').dropdown({
  limitCount: 40,
  multipleMode: 'label',
  choice: function () {
    console.log(arguments,this);
  }
});
```


## Example

[https://janking.github.io/dropdown/](https://janking.github.io/dropdown/)
