# Ubuntu系统硬盘挂载

1.检查硬盘：
    
    sudo fdisk -l

确保找到您要挂载的硬盘设备（例如，/dev/sdb）

2.创建挂载点：

    sudo mkdir /mnt/mydisk

这将在/mnt目录下创建名为"mydisk"的目录作为挂载点

3.挂载硬盘：

挂载硬盘到挂载点：

    sudo mount /dev/sdb /mnt/mydisk

将"/dev/sdb"替换为您要挂载的硬盘设备的路径

4.自动挂载：

在系统启动时自动挂载硬盘，需要进行一些额外的配置,执行以下命令来打开fstab文件进行编辑：

    sudo nano /etc/fstab

在文件的末尾添加以下行，用于描述要挂载的硬盘设备和挂载点的信息：

    /dev/sdb   /mnt/mydisk   ext4   defaults   0   0

保存并关闭文件

5.卸载硬盘：

如果想要卸载挂载的硬盘，可以执行以下命令：

    sudo umount /mnt/mydisk
