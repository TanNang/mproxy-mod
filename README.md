# http代理 - 自定义Host头域

## 使用
- 编译：`gcc -o mproxy mproxy-mod.c`；
- 启动mproxy：`./mproxy -l 8080 -m RHost: -d`；
- 关闭mproxy：`pkill mproxy`；
- tiny.conf：参考`tiny.conf`；

## 注意
- 自定义头域 "-m" 可指定为任意适当长度的字符串；
- http 请求中，自定义头域须紧跟 Host 头域，https 无要求；
