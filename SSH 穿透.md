### SSH 穿透

- 参考链接

  [LCX_portmap]: https://blog.csdn.net/wyvbboy/article/details/61921773
  [portmap_code]: https://github.com/juzeon/fire
  [LCX]: https://dfkan.com/1204.html

### 测试环境

- 一台公网VPS，IP：188.131.143.61
- 一台树莓派，已开启ssh服务，并在sshd_config文件中增加了端口2222



### portmap编译

- git clone https://github.com/juzeon/fire 

- 在公网服务器和树莓派上分别编译portmap.c
-  gcc portmap.c -o portmap
- chmod u+x portmap

### 在公网服务器上

- 将公网服务器端口5555映射到公网服务器端口2222，随时接受发送给5555端口的数据，并转发多2222端口

sudo ./portmap -m 2 -h1 0.0.0.0 -p1 5555 -h2 0.0.0.0 -p2 2222

### 在树莓派上

- sudo ./portmap -m 3 -h1 127.0.0.1 -p1 2222 -h2 188.131.143.61 -p2 5555
- 将本地SSH端口2222的数据转发到服务器端口5555

### ### 穿透连接

- ssh -p 2222 pi@188.131.143.61
- 其中pi为树莓派登录用户名
- 2222为服务器转发端口