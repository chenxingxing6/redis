该自述文件只是快速的*快速入门*文档。您可以在[redis.io]（https://redis.io）上找到更详细的文档。

什么是Redis？
--------------

Redis通常被称为*数据结构*服务器。这意味着Redis通过一组命令提供对可变数据结构的访问，这些命令使用带有TCP套接字和简单协议的* server-client *模型发送。因此，不同的进程可以以共享的方式查询和修改相同的数据结构。

Redis中实现的数据结构具有一些特殊属性：

* Redis始终将它们存储在磁盘上，即使它们始终被提供并修改到服务器内存中也是如此。这意味着Redis速度很快，但这也是非易失性的。
*数据结构的实现会提高内存效率，因此与使用高级编程语言建模的相同数据结构相比，Redis内部的数据结构可能使用较少的内存。
* Redis提供了许多自然可以在数据库中找到的功能，例如复制，持久性的可调级别，集群，高可用性。

另一个很好的例子是将Redis视为memcached的一个更复杂的版本，其中的操作不仅是SET和GET，而且是与复杂数据类型（如列表，集合，有序数据结构等）一起使用的操作。

如果您想了解更多信息，请参见以下选定的起点列表：

* Redis数据类型简介。 http://redis.io/topics/data-types-intro
*直接在浏览器中尝试Redis。 http://try.redis.io
* Redis命令的完整列表。 http://redis.io/commands
* Redis官方文档中还有更多内容。 http://redis.io/documentation

建筑Redis
--------------

Redis可以在Linux，OSX，OpenBSD，NetBSD，FreeBSD上进行编译和使用。
我们支持大端和小端架构，并且都支持32位
和64位系统。

它可以在Solaris衍生系统（例如SmartOS）上编译，但是我们
*尽最大努力*支持此平台，并且不能保证Redis会
可以在Linux，OSX和\ * BSD中正常工作。

它很简单：

    ％制造

您可以使用以下命令运行32位Redis二进制文件：

    ％使32位

构建Redis之后，最好使用以下方法进行测试：

    ％进行测试

修复依赖项或缓存的构建选项的构建问题
---------

Redis有一些依赖关系，包含在`deps`目录中。
make不会自动重建依赖关系，即使
依赖项的源代码更改。

当您使用`git pull`更新源代码时，或
依赖关系树以任何其他方式修改，请确保使用以下内容
命令以真正清理所有内容并从头开始重建：

    使distclean

这将清除：jemalloc，lua，hiredis，linenoise。

另外，如果您强制使用某些构建选项（例如32位目标），则无需C编译器
优化（出于调试目的）和其他类似的构建时间选项，
这些选项将无限期地缓存，直到您发出`make distclean`为止。
命令。

解决构建32位二进制文​​件的问题
---------

如果在使用32位目标构建Redis之后需要重建它
目标为64位或相反的情况下，您需要执行
Redis发行版的根目录中的make distclean。

如果在尝试构建Redis的32位二进制文​​件时出现构建错误，请尝试
以下步骤：

*安装软件包libc6-dev-i386（也尝试使用g ++-multilib）。
*尝试使用以下命令行而不是`make 32bit`：
  make CFLAGS =“-m32 -march = native” LDFLAGS =“-m32”`

分配者
---------

通过设置构建Redis时选择非默认内存分配器
“ MALLOC”环境变量。 Redis编译并与libc链接
默认情况下，malloc，但jemalloc是Linux上的默认值
系统。选择此默认值是因为事实证明jemalloc具有较少的值
比libc malloc碎片问题。

要强制针对libc malloc进行编译，请使用：

    ％使MALLOC = libc

要在Mac OS X系统上针对jemalloc进行编译，请使用：

    ％使MALLOC = jemalloc

详细构建
-------------

默认情况下，Redis将使用用户友好的彩色输出进行构建。
如果要查看更详细的输出，请使用以下命令：

    ％使V = 1

运行Redis
-------------

要使用默认配置运行Redis，只需键入：

    ％cd src
    ％./redis-server

如果要提供redis.conf，则必须使用其他命令来运行它。
参数（配置文件的路径）：

    ％cd src
    ％./redis-server /path/to/redis.conf

可以通过直接传递参数来更改Redis配置
作为使用命令行的选项。例子：

    ％./redis-server-端口9999-副本127.0.0.1 6379
    ％./redis-server /etc/redis/6379.conf --loglevel调试

使用以下命令，也支持redis.conf中的所有选项作为选项
行，名称完全相同。

玩Redis
------------------

您可以使用redis-cli来玩Re
