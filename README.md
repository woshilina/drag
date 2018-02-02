### 一.功能介绍:
##### 1. 可多次将图片(这里是一个大黑色圆点),拖拽到画布上.
##### 2. 点击图片左半部分可以实现点与点之间连线.
##### 3. 点击图片右半部分可以实现图片的拖拽,上边的线也会随之被推动.

### 二.遇到的问题及解决方法:
##### 1. 默认拖放效果会把图片拖放到画布,画布上边的图片就不再存在,如何实现可以多次拖拽,图片仍然存在?
设置拖放操作效果为copy

```
ev.dataTransfer.dropEffect="copy"
```
可能得值:
- copy(复制到新位置)
- move(移动到新位置);
- link(在新位置建立一个链接)
- none(不能被拖放)

##### 2. 拖拽时鼠标在画布移动时拖拽的点和线如何随鼠标位置实时改变?
使用htmlDOM方法setInterval(code,millisec),按指定周期(毫秒计)调用code函数或计算code表达式

```
timer1 = setInterval(drawScreen(endx, endy), 1000 / 300);//每1000/300毫秒执行一次drawScreen()函数,此函数作用是清除画布内容再画上位置改变后的内容(点和线)
```
通过clearInterval()停止调用函数
```
clearInterval(time1);
```
##### 3. 如何实现拖拽点时点和线同时更新?
思路:将目标点上的线放到一个新的数组,记录线的起点和终点位置,并在所有线的数组中清空(不是真正的删除,只是该索引下的内容为空),这样被拖拽的线和未被拖拽的线分别存在两个数组中,再分别画出点和线.

ps:在鼠标点击时间函数里要清空被拖拽的线的数组(dragarr)
