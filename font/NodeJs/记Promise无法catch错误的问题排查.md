在一个类Node项目中(autojs项目),最开始的方法时同步的
```js
function testTask(){
  log('恭喜您成功完成测试任务');
}

try{
  testTask();
}catch(error){
  log('测试任务在执行过程中发生了错误:'+JSON.stringify(error));
}
```
>14:32:51.243/D: 恭喜您成功完成测试任务

我们对测试任务稍作修改,通过手动抛出一个异常来模拟实际环境中的错误
```js
function testTask(){
  throw Error('测试');
  log('恭喜您成功完成测试任务');
}
```

>14:35:02.500/D: 测试任务在执行过程中发生了错误:{"message":"测试"}

紧接着,由于方法发生了变更,它变成了异步模式
```js
//项目的迭代导致新增了一些子任务
function longSubTask(){
  log('子任务完成了');
}

async function testTask(){
  await longSubTask();
  log('恭喜您成功完成很长的测试任务');
}

try{
  testTask();
}catch(error){
  log('测试任务在执行过程中发生了错误:'+JSON.stringify(error));
}
```
>14:51:18.242/D: 子任务完成了\
>14:51:18.263/D: 恭喜您成功完成很长的测试任务

看起来一切都很正常,但是细心的朋友会发现我们 方法虽然声明了async,但是testTask方法在被调用的时候没有使用await修饰符.`这里就有个隐患`,就是如果async方法内部发生了错误,错误信息是catch不到的.也就是上面的try/catch是无法进入catch分支的.

我们重新改造下子任务
```js
function longSubTask(){
  undefinedMethod()//尝试调用一个未定义的方法
  log('子任务完成了');
}
```

这个时候发现.testTask任务无法运行了而且也不报错。

#### 问题
我们发现,最终的版本中,testTask任务无法运行了而且也不报错。

#### 原理&总结
testTask方法被async修饰,此时如果我们去获取testTask()的类型,会发现resultType输出Object(其实就是Promise),而由于我们没有调用Promise的reject/resolve函数,导致最终的结果一直被阻塞.从而无法进入catch分支
```js
let resultType = testTask();
log('返回值类型是:'+resultType);
```
我们对调用方式进行了改造
```js
async function correctInvoke(){
  try{
    await testTask();//await只能在async函数内部使用
  }catch(error){
    log('测试任务发生了错误:'+JSON.stringify(error));
  }
}

correctInvoke();
```
>这里可以看出,
1. await必须被async函数包裹
2. await只关心resolve的消息,如果过程中发生错误需要自行catch

通过上面的分析我们已经知道`错误原因无法显示是因为Promise未调用resolve/reject函数导致的`,在实际的编码过程中,我们需要注意的是返回的对象是不是Promise类型.如果是,Promise是否有正常调用resolve/reject方法.否则就会遇到本章篇幅所描述的问题.
