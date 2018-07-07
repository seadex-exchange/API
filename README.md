# 入门引导

## Seadex API概述


用户提供简单而又强大的API接口服务，旨在帮助用户快速高效的将 Seadex（Seadex.io）交易功能整合到自己应用当中。

通过 API 您可以快速实现如下功能

市场最新行情
交易信息
账户信息
买方卖方深度信息
订单信息
快速买进卖出
撤销订单
所有请求基于 http 协议，请求头信息中 contentType 需要统一设置为: 'application/x-www-form-urlencoded'，访问的根URL：http://api.seadex.io/

例如：

contentType:'application/x-www-form-urlencoded'
如果在使用过程中有任何问题，请联系我们技术讨论电报群：Seadex官方API技术交流群：325248096，我们将为您做出最权威的解答。

Getting Started
Seadex为用户提供了三种调用接口的方式，开发者可根据自己的使用场景和偏好选择适合自己的方式来查询行情、进行交易或提现。

REST API
REST，即Representational State Transfer的缩写，是目前最流行的一种互联网软件架构。它结构清晰、符合标准、易于理解、扩展方便，正得到越来越多网站的采用。其优点如下：

在RESTful架构中，每一个URL代表一种资源；
客户端和服务器之间，传递这种资源的某种表现层；
客户端通过四个HTTP指令，对服务器端资源进行操作，实现“表现层状态转化”。
建议开发者使用REST API进行币币交易或者资产提现等操作。

WebSocket API    
Seadex同样为用户提供了快速高效的WebSocket行情接口，

WebSocket是HTML5一种新的协议(Protocol)。它实现了客户端与服务器全双工通信，使得数据可以快速地双向传播。通过一次简单的握手就可以建立客户端和服务器连接，服务器根据业务规则可以主动推送信息给客户端。其优点如下：

客户端和服务器进行数据传输时，请求头信息比较小，大概2个字节;
客户端和服务器皆可以主动地发送数据给对方；
不需要多次创建TCP请求和销毁，节约宽带和服务器的资源。
强烈建议开发者使用WebSocket API获取市场行情和买卖深度等信息。

开启API权限    
用户的API权限在网站的安全->API内获取。点击申请API即可获得，其中apiKey是Seadex提供给API用户的访问密钥，secretKey用于对请求参数签名的私钥。

注意： 请勿向任何人泄露这两个参数，这两个参数关乎您账号的安全。

生成待签名字符串
用户提交的参数除sign外，都要参与签名。待签名字符串要求按照参数名进行排序（首先比较所有参数名的第一个字母，按abcd顺序排列，若遇到相同首字母,则看第二个字母, 以此类推。）

例如：对于如下的参数进行签名

string[] parameters={
  "api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c"，
  "symbol=eth_btc",
  "type=buy",
  "price=680",
  "amount=1.0"
}; 
生成待签名字符串为：

amount=1.0&api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c&price=680&symbol=eth_btc&type=buy.
MD5签名
在MD5签名时,需要私钥secretKey参与签名。将待签名字符串添加私钥参数生成最终待签名字符串。 例如：

amount=1.0&api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c&price=680&symbol=eth_btc&type=buy&secret_key=secretKey 
注意&secret_key=secretKey 为签名必要参数。

利用32位MD5算法 对最终待签名字符串进行签名运算,从而得到签名结果字符串(该字符串赋值于参数sign)，MD5计算结果中字母全部大写。
