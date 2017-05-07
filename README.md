## mproxy-mod
支持http和https自定义头域代理的mproxy实现

## 更新
重新修改了源码，在保证其原有功能的基础上，新加了两个参数"-r"和"-m"

### `-r <ip:port>`  将流量无条件转发至指定的[服务器:端口]
`./mproxy -l 8080 -r 127.0.0.1:443`

"-r"参数转发流量时，不转发CONNECT(http_tunnel)连接的header信息;
而"-h"参数是不处理数据，全部转发(header+data)

### `-m <real_host string>` 指定真实Host头域关键字，忽略原Host头域
`./mproxy -l 8080 -m ZFL:`

> 注意：-h -r -m三个参数尽量不要一起用，优先级-h > -m > -r

`/mproxy -l 8080 -h xxxx -m xxxx -r xxxx`   只有-h起作用，-m和-r将失效

`./mproxy -l 8080 -m ZFL: -r 127.0.0.1:443`
只有当连接header中不包含"ZFL:"时，才会转发至127.0.0.1:443;
如果包含，则仍将转发至"ZFL:"所确定的地址

## 使用
- 编译          `gcc -o mproxy mproxy-mod.c`
- 启动mproxy    `./mproxy -l 8080 -m ZFL: -d`
- 关闭mproxy    `pkill mproxy`
- tiny.conf     参考`tiny.conf`

## 注意
- 自定义头域"-m"可指定为任意适当长度的字符串
- http请求中，自定义头域`ZFL: [H]\r\n`须紧跟`Host: m.client.10010.com\r\n`; https无要求


**注: 源码来源于[examplecode/mproxy](https://github.com/examplecode/mproxy) 我只是稍加整理**
