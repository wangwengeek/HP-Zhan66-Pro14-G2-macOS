## OC-引导多系统

- 设置位置：`Misc\Entries`

- 定义启动项

  - `Comment`：一个有意义的名称。
  - `Enabled`：允许开关。
  - `Name`：引导时显示的名称。
  - `Path`：被引导系统的绝对路径。

- 示例：

  按照`定义启动项`的格式要求填写所有内容。其中`path`格式像这样：

  示例1：

  ```
  PciRoot(0x0)/Pci(0x14,0x0)/USB(0xE,0x0)/HD(1,GPT,FBAB0AB8-698F-11E9-8DC7-93AD5ED2C040,0x800,0x1A716B)/\EFI\BOOT\BOOTX64.EFI
  ```

  示例2：

  ```
  PciRoot(0x0)/Pci(0x1D,0x0)/Pci(0x0,0x0)/NVMe(0x1,00-00-00-00-00-00-00-00)/HD(1,GPT,8763DD59-B7D6-4734-9B01-D7BCD42ECDDA,0x800,0x96000)/\EFI\Microsoft\Boot\bootmgfw.efi
  ```

  示例1为移动硬盘的Windows系统的绝对路径（自带EFI，可引导）。

  示例2为驱动器不同分区的Windows系统的绝对路径。`Microsoft`是可引导windows的文件夹。

- 获取`path`的方法

  - 终端确认启动分区的UUID

    终端输入`diskutil list`，确认启动分区硬盘标识符，如：`disk2s1`。

    终端输入`diskutil info disk2s1`进一步确认`启动分区的UUID`，如：

    ```
    ......
    Disk / Partition UUID:     FBAB0AB8-698F-11E9-8DC7-93AD5ED2C040
    ......
    ```

  - 获得完整的`path`

    - 安装`NOOPT`或者`DEBUG`版本的`OpenCore`（BOOTx64.ef`和OpenCore.efi）。
    - 设置Debug选项，提取日志文件：EFI根目录\opencore-YYYY-MM-DD-HHMMSS.txt。
      - `Misc\Debug\DisableWatchDog`=`true`
      - `Misc\Debug\Target`=`65`
    - 打开opencore-YYYY-MM-DD-HHMMSS.txt文件，搜索前文已经确认的`启动分区的UUID`。
    - 参考示例获得完整的`path`。

- 注：Clover , Grub 等其他系统可以参照上述示例添加引导项目，达成以OC为主的多系统引导管理器。


