## OC-解锁MSR、setup_var方法

- 什么是`MSR`寄存器

  MSR是Model Specific Register的全称。它是CPU的一组寄存器，是为了控制CPU工作环境、工作状态、温度控制、性能监控等方面而设置的专用寄存器。不同的CPU型号，它的MSR寄存器可能不一样。当发布一款新的CPU时，也可能引入新的MSR寄存器。每个MSR寄存器都会有一个相应的ID（MSR寄存器地址），即MSR-Index。通过这个ID就可以对MSR寄存器进行读写操作。读写过程是透明的，可以在BIOS、UEFI、系统中完成。
  
- `MSR(0xE2) `、`PKG_CST_CONFIG_CONTROL`、`CFG Lock`、`MSR Lock`

  MSR寄存器的第`21`位通常是锁定状态，因为Windows不使用它。但对MAC而言，CPU电源管理和`21`位有关，无论是早期机器的AppleIntelCPUPowerManagement.kext还是新机器的XNU内核，只要对`21`位进行写操作就会导致系统崩溃。所以，使用MAC系统则必须对`21`位解锁或者使用相关补丁。

  通常，`21`位被称为`MSR(0xE2)`、OC称之为`PKG_CST_CONFIG_CONTROL`。

  有的机器BIOS设置了该选项，叫`CFG Lock`或者`MSR Lock`。

- OpenCore查看`MSR(0xE2)`状态

  - 下载并安装`VerifyMsrE2.efi`到EFI\OC\tools。
  - Config\Misc\Tools下正确添加`VerifyMsrE2.efi`的列表。
  - OpenCore引导界面选择`VerifyMsrE2.efi`条目，回车。

- `解锁MSR`

  - `BIOS`

    - 如果BIOS提供了`CFG Lock`（或`MSR Lock`）选项，令`CFG Lock`（或`CFG Lock`）=`disable`。
    - 如果BIOS没有`CFG Lock`（或`MSR Lock`）选项，修改BIOS文件重刷BIOS。`注意：刷BIOS有风险`。

  - `CMOS`

    通过改写CMOS内容`解锁MSR`，见后文***`setup_var`方法***。下面2种情况CMOS信息将丢失：

    - 重刷BIOS。
    - CMOS电池掉电超过一定时间。

  - `config补丁`

    - 4代之前的机器，`Kernel\Quirks\AppleCpuPmCfgLock`=`true`。同clover勾选`AppleIntelCPUPM`。
    
    - 4代及4代之后的代机器，`Kernel\Quirks\AppleXcpmCfgLock`=`true`。同clover勾选`KernelPM`。
    
      

## 其他MSR设置

- `Kernel\Quirks\AppleXcpmExtraMsrs`

  对于不支持原生XCPM的处理器，禁止访问多重MSR寄存器。通常适用于`Haswell-E`, `Broadwell-E`, `Skylake-X`，或者其他相似的CPU。更多的关于XCPM补丁参见acidanthera/bugtracker#365。

- `UEFI\Quirks\IgnoreInvalidFlexRatio`

  如果BIOS是AMI `APTIO IV`版本，MSR寄存器`MSR_FLEX_RATIO (0x194)` 可能包涵无效值并导致启动失败，请设置`IgnoreInvalidFlexRatio` = `true`。

  `注意`：虽然该选项对未受影响的机器不会造成伤害，但还是建议在这类机器上不要使用它。

## 附：`setup_var`方法

`setup_var`方法可以`开启AHCI`、调整`DVMT内存`、`解锁MSR`。

- 提取BIOS文件，一般是`.ROM`。

- 准备相关工具软件：`UEFITool`、`ifrextract`。

- 查找确认偏移量地址和内容：

  - 用`UEFITool`打开`.ROM`文件。

  - 以文本方式搜索`CFG Lock`或者`MSR Lock`。

  - 双击`search`条目，弹出`Setup`下面的`PE32 image section`。

  - 鼠标右击`PE32 image section`，选中`Extract body…`，保存为`bin`格式文件（文件名随意）。

  - 把`ifrextract`和`bin`文件放到桌面，执行终端命令，将`bin`文件转化为`TXT`文件。

    终端：

    ``` 
    cd ~/desktop
    ./ifrextract 文件名.bin 文件名.txt
    ```
  
  - 打开`TXT`文件，搜索`CFG Lock`或者``MSR Lock``，如：
  
    ```
    CFG Lock, VarStoreInfo (VarOffset/VarName): 0x4ED, VarStore: 0x1...
    One Of Option: Disabled, Value (8 bit): 0x0...
    One Of Option: Enabled, Value (8 bit): 0x1...
    ```
  
    确认偏移量地址：`0x4ED`，当前值：`0x1`。如果将`0x1`修改为`0x0`，即可达到`解锁MSR`目的。
  
- 进入shell模式，输入解锁命令，如：输入`setup_var 0x4ED 0x0`回车。

- 如果需要`开启AHCI`、调整`DVMT内存`的话，在`TXT`文件中搜索`AHCI`、`DVMT`以确认偏移量地址和内容。


  `注意事项`：如果因操作错误或其他原因导致无法开机，请拆除所有电源（AC、电池、COMS电池）等待数分钟后再重新安装所有电源。