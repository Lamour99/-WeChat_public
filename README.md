"微信公众号的开发" 

1.cheapter01
需要用ngrok把本地的地址通过内网穿透暴露出去

验证服务器的有效性
1.微信服务器知道开发者服务器是哪个
   -测试号管理页面上填写url开发者服务区地址
   -使用ngrok内网穿透 将本地端口号开启的服务映射外网跨越访问一个网址
   -ngrok http 3000
  -填写token
   -参与微信签名加密的一个参数
  2.开发者服务器 - 验证消息是否来自于微信服务器
   目的：计算得出signature微信加密签名，和微信传递过来的signature进行对比，如果一样，说明消息是来自于微信服务器，如不一样，说明不是
   1.将参与微信加密签名的三个参数（timestamp，nonce，token）按照字段序排序并组合在一起
   2.将数组里所有参数拼接成一个字符串，进行cha1加密
   3.加密完成就生成一个signature，和微信发送过来的进行对比
     -如果一样，说明消息来自于微信服务器，返回echostr给微信服务器
     -如果不一样，说明不是微信服务器发送的消息，返回error
