# console

```js
/* 清空控制台 */
console.clear(); 
/* 向控制台输出一条信息，该信息包含一个表示“信息”的图标，和指向该行代码位置的超链接。 */
console.info(); 
/* 同 info。区别是图标与样式不同。 */
console.warn(); 
/* 同 info。区别是图标与样式不同。error 实际上和 throw new Error() 产生的效果相同，使用该语句时会向浏览器抛出一个 js 异常。 */
console.error(); 
/* 断言，测试一条表达式是否为真，不为真时将抛出异常（断言失败）。 */
console.assert(); 
/* 输出一个对象的全部属性（输出结果类似于 DOM 面板中的样式）。 */
console.dir(); 
/* 输出一个 HTML 或者 XML 元素的结构树，点击结构树上面的节点进入到 HTML 面板。 */
console.dirxml(); 
/* 输出 Javascript 执行时的堆栈追踪。 */
console.trace(); 
/* 输出消息的同时打开一个嵌套块，用以缩进输出的内容。调用 console.groupEnd() 用以结束这个块的输出。 */
console.group(); 
/* 同 console.group(); 区别在于嵌套块默认是收起的。 */
console.groupCollapsed(); 
/* 计时器，当调用 console.timeEnd(name);并传递相同的 name 为参数时，计时停止，并输出执行两条语句之间代码所消耗的时间（毫秒）。 */
console.time(); 
/* 与 profileEnd() 结合使用，用来做性能测试，与 console 面板上 profile 按钮的功能完全相同。 */
console.profile(); 
/* 输出该行代码被执行的次数，参数 title 将在输出时作为输出结果的前缀使用。 */ /*     分组 */
console.count(); 

```