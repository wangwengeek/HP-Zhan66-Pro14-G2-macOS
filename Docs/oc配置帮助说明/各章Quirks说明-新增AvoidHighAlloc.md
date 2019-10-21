## 各章Quirks说明

1. ACPI\Quirks（第四章）

   - **`FadtEnableReset`**【推荐值=false】

     重置<u>*FADT*</u>表单的“register and flag“标志，解决早期机器重启和关机问题。除非需要，否则不推荐。

   - **`NormalizeHeaders`**【推荐值=false】

     清除ACPI的“header”字段以解决系统崩溃问题。这个问题在10.14已经得到解决。

   - **`RebaseRegions`**【推荐值=false】

     尝试重新定位ACPI内存区域。ACPI地址是动态生成的，随硬件的变动或者升级而改变，修改它们非常危险。除非绝对需要，否则不要使用。

   - **`ResetHwSig`**【推荐值=false】

     重置<u>*FACS*</u>表单的“Hardware Signature”为0。解决因从休眠中唤醒后该项不一致而导致的一些问题。

     打开原始<u>*FACS*</u>文件，查看“Hardware Signature”是否为0，如果不为0，选择此项=true 。

     如小新<u>*FACS*</u>：

     `[008h 0008   4]           Hardware Signature : 690E59C1`

   - **`ResetLogoStatus`**【推荐值=false】

     置<u>*BGRT*</u>表单的“Displayed”标志位=false。
     
     

2. Kernel\Quirks（第六章）

   - **`AppleCpuPmCfgLock`**【推荐值=false】

     禁止修改AppleIntelCPUPowerManage-ment.kext中的PKG_CST_config_Control(0xE2)MSR，当它被写入时，通常会导致系统崩溃。

     注：新的机器提供了对应的CFG设置，设置为Lock即可。

   - **`AppleXcpmCfgLock`**【推荐值=false】

     禁止修改XNU内核中的PKG_CST_config_CONTROL(0xE2)MSR，当它被写入时，通常会导致系统崩溃。

   - **`AppleXcpmExtraMsrs`**【推荐值=false】

     支持原生XCPM的CPU（4代以上）才使用。不支持原生XCPM的CPU严禁使用。

   - **`CustomSMBIOSGuid`**【推荐值=false】

     戴尔笔记本专用补丁（慎用）。

   - **`DisableIoMapper`**【推荐值=false】

     同drop DMAR作用相同。首选这个选项，尽可能不使用drop DMAR。

   - **`ExternalDiskIcons`**【推荐值=false】

     橙色磁盘（AHCI）补丁。尽可能不勾选此项。

   - **`LapicKernelPanic`**【推荐值=false】

     panic内核补丁1。

   - **`PanicNoKextDump`**【推荐值=false】

     panic内核补丁2。适用于10.13以上。

   - **`ThirdPartyTrim`**【推荐值=false】

     TRIM补丁。应尽可能避免适用。

   - **`XhciPortLimit`**【推荐值=false】

     USB端口数量限制补丁。应尽可能避免适用。

     

3. UEFI\Quirks（第十章）
   - **`ExitBootServicesDelay`**【推荐值=0】
   
     某种情况在EXIT_boot_services事件之后会无法访问SATA控制器，增加3-5秒可解决问题。
   
   - **`IgnoreInvalidFlexRatio`**【推荐值=false】
   
     当MSR寄存器(0x194)包涵无效值时，将导致引导失败。
   
     注意：通常情况不建议使用它，即使选择此项不会造成有什么影响。
   
   - **`IgnoreTextInGraphics`**【推荐值=false】
   
     当控制台输出与文本模式不同时，会导致UI损坏。将此选项设置为true将丢弃所有文本输出。
   
     注意：此选项可能隐藏屏幕上的错误消息。可能需要将ConsoleControl设置为true才能工作。
   
   - **`ProvideConsoleGop`**【推荐值=false】
   
     引导时，如果丢失GOP(Graphics Output Protocol)，需要添加它。
   
     注意：一些驱动程序，如AptioMemoryFix，可能提供相同的功能。这些驱动程序不能保证遵循相同的逻辑，如果有必要使用此选项，则首选此选项。
   
   - **`ReleaseUsbOwnership`**【推荐值=false】
   
     如果USB控制器与驱动程序无法分离，启动时可能会冻结。选择true将尝试USB控制器从驱动程序分离。
   
     除非需要，否则不推荐。
   
   - **`RequestBootVarRouting`**【推荐值=false】
   
     将 EFI 的 NVRAM 重定向到 OC 的 NVRAM。
   
   - **`SanitiseClearScreen`**【推荐值=false】
   
     当使用大显示器(例如2K或4K)时，试图清除屏幕时将分辨率重置为安全值(如1024x768)。
   
     注意：`UEFI\Protocols\ConsoleControl`可能需要设置为true才能工作。而且`Misc\Boot\ConsoleMode`要设置为空。
   
   - `AvoidHighAlloc`【推荐值=false】
   
     设置true时，允许引导过程访问更高内存区域。除非必须，否则=false 。
