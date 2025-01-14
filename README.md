
# Hadoop Native Library for macOS

这个仓库提供了一些 macOS 系统下的 Hadoop 本地库，可以消除在 macOS 下运行 Hadoop 程序时的警告：

```shell
WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform...
using builtin-java classes where applicable
```

当前目录下的 `hadoop-x.x.x` 均为 Intel 芯片的本地库文件，Apple M1、Apple M2 等 ARM 芯片请使用 [ARM](./ARM) 目录下的文件。

## 使用方法

将 `hadoop-x.x.x/lib/native` 下的文件，替换到本地`${HADOOP_HOME}/lib/native` 中（删除原来的所有文件）。

不用重启 Hadoop 集群，即可验证警告消失（Hadoop-3.2.1 为例）：

![hdfs-ls](img/hdfs-ls.png)

查看 Hadoop 支持的本地库信息：

```shell
cd ${HADOOP_HOME}
bin/hadoop checknative -a

# 主要结果
Native library checking:
hadoop:  true /Users/healchow/bigdata/hadoop-3.2.1/lib/native/libhadoop.dylib
zlib:    true /usr/lib/libz.1.dylib
zstd  :  true /usr/local/Cellar/zstd/1.5.0/lib/libzstd.1.5.0.dylib
snappy:  true /usr/local/Cellar/snappy/1.1.4/lib/libsnappy.1.dylib
lz4:     true revision:10301
bzip2:   false
openssl: false EVP_CIPHER_CTX_reset
ISA-L:   false Loading ISA-L failed: Failed to load libisal.2.dylib (dlopen(libisal.2.dylib, 9): image not found)
```

![hadoop-checknative](img/hadoop-checknative.png)

其中报错是因为本地没有 snappy 压缩相关的库，暂时忽略。

## 可用版本

经自我测试，可用的版本如下（欢迎大家补充）：

|     版本号     |   是否可用   |
| :-----------: | :--------: |
| hadoop-2.7.3  |     未知    |
| hadoop-2.7.7  |     未知    |
| hadoop-2.8.5  |     未知    |
| hadoop-2.9.2  |     未知    |
| hadoop-3.1.3  |     未知    |
| hadoop-3.2.1  |  **可用**   |
| ...           | ...        |


## 参考仓库

https://github.com/mingsquall/native-hadoop-library

https://github.com/janlle/mac-hadoop-native-lib-mojove
