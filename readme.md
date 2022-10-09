# 环境构建

## centos

假设处于root用户，其他权限用户请自行sudo，目录也可以自己酌情更改

shell里面逐句执行：

```
yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm libbsd libbsd-devel
curl -P ~/ http://www.apuebook.com/src.3e.tar.gz
cd ~/
tar -zxvf src.3e.tar
cd apue.3e/
cp lib/error.c include/
vi include/apue.h
```

在打开文件的

```
#endif /* _APUE_H */
```

语句前添加一行

```
#include "error.c"
```

保存退出，之后shell继续逐句执行

```
make
cp include/apue.h include/error.c /usr/include/
cp lib/libapue.a /usr/local/lib/
```

之后便可以引入头文件"apue.h"

在编译的时候加上动态库连接-lapue,还有头文件库，但是通用的apue.h已经拷贝到gcc
搜索链接库的时候默认路径中，不用担心找不到，除非有依赖才使用参数附加头文件路径。
