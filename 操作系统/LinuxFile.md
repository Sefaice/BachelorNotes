# Linux中的软链接与硬链接

[Linux 的文件与目录](https://www.ibm.com/developerworks/cn/linux/l-cn-hardandsymb-links/index.html)

UNIX 系统中除进程之外的一切皆是文件，而文件在Linux上被分为两个部分：用户数据 (user data) 与元数据 (metadata)，元数据的inode号，即索引节点号，是文件的唯一标识符。

可通过`stat`或`ls -i`命令查看文件的inode。

为解决文件的共享使用，Linux 系统引入了两种链接：硬链接 (hard link) 与软链接（又称符号链接，即 soft link 或 symbolic link）。

若一个 inode 号对应多个文件名，则称这些文件为**硬链接**，即同一个文件（inode）对应多个文件名。硬链接可由命令`link oldfile newfile`或`ln oldfile newfile`创建，这样创建的文件有相同的inode号。

若文件用户数据块中存放的内容是另一文件的路径名的指向，则该文件就是**软连接**，软链接有自己的indoe和数据块。可通过`ln -s oldfile new file`命令创建软连接。

当创建多个硬链接指向同一文件时，该文件和新建的硬链接文件的Link，即链接计数器的值会对应增加，删除硬链接文件也会对应减少，说明**链接计数器Link的值就是指向这一inode的文件名个数**。

再建立指向该文件的软链接，软链接文件的Link值为1，原文件Link值不变，无论原文件的硬链接数如何改变，软链接的Link值始终不变，因为只有一个文件指向了它的inode，而若新建一个指向该软链接文件的硬链接，它的Link值就变成2了，这也继续验证了Link值就是inode对应文件名的个数。