# 简单的WEB服务器（MVC版本）

额 这个是简单的web服务器实现前端设备访问连接功能的服务器，使用java--Spring MVC结构进行编写

秉着不重复造轮子的原则（实际上我就是懒┭┮﹏┭┮），里面一些配置文件用的是现成的

当然，这里面的关键还是controller等那些嘛

这个是当时第一个版本写的，所以一些命名规则其实很离谱，但也不想改了

## 实现功能

实现三个功能——对数据库进行crud操作（当然一开始写了d后来把d删掉了）

#### 对数据库“写”操作

前端设备获取到GPS信息后通过POST请求相应的网址（xxx.xxx.xx.xxx/mqttLoad/testMqtt）

上传内容——这个根据你数据库所写的格式来判断嘛，我数据库写了五个字段

“id 设备号 经度  维度 时间“

上传JSON字符串

统一为JSON格式

{

​	“imei”:"xxx",

​	"lng":"xxx",

​	"lat":"xxx",

​	"t":"格式化时间戳"

}

（id自增懂的都懂）

![image-20220205200111643](D:\java资料\web服务器\WEB-Server\img\1.png)



#### 取出某设备号最近的一次记录

这个是  想要的 查看该设备当前所在位置，其实按照逻辑来说 查看当前所在位置应该是手机请求端发送（设备号+当前时间戳），但后面想了想，就找最近的嘛，反正返还的时候也带着时间，让前端的处理逻辑简单一点。

xxx.xxx.xx.xxx:8080/mqttLoad/getSinGps?imei=xxx

![image-20220205200435353](D:\java资料\web服务器\WEB-Server\img\2.png)

#### 获取一段时间内的位置-->xxx.xxx.xx.xxx:8080/mqttLoad/getGps?imei=xxx&sTime=xxx&eTime=xxx

imei=xxx&sTime=xxx&eTime=xxx
通过get请求传递三个参数（imei，起始时间sTime，终止时间eTime），获取这段时间内的gps信息和上传时间，示例如下

![image-20220205200542085](D:\java资料\web服务器\WEB-Server\img\3.png)

#### 提醒自己的点

其实这些搭建服务器并不难，复杂的是mqtt作为前端移动设备中间件的问题，后面记得提醒自己上传mqtt等相关的东西