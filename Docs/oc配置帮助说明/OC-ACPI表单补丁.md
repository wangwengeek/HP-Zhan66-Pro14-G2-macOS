## OC-ACPI表单补丁

提取ACPI，查看是否存在表单：`BGRT.aml`、`FACS.aml`、`FADT.aml`、`DMAR.aml`。如果有这些表单或部分表单，可能需要相关修补和设置。

## ACPI\Quirks

- `FadtEnableReset`【FADT.aml】

  重置<u>`FADT`</u>表单的`register and flag`标志位。

  该选项解决早期机器重启和关机问题。除非需要，否则不建议使用。

- `NormalizeHeaders`

  清除ACPI的`header`字段以解决引导过程崩溃问题。这个问题在10.14+已经得到解决。

- `RebaseRegions`

  尝试重新定位ACPI内存区域。

  ACPI地址是动态生成的，随硬件的变动或者升级而改变。除非绝对必要，否则请勿使用。

- `ResetHwSig`【FACS.aml】

  重置<u>`FACS`</u>表单的`Hardware Signature`为`0`。

  示例：

  ```
  Hardware Signature : 5453DB17
  ```

  某些机器因重启后无法维持硬件签名而导致从休眠状态唤醒的问题。出现此问题设置`ResetHwSig` = `true` 。

- `ResetLogoStatus`【BGRT.aml】

  重置<u>`BGRT`</u>表单的`Displayed`标志位=`0`。

  示例：

  ```
  Displayed : 1
  ```

  当机器的ACPI表单有`BGRT.aml`，并无法处理屏幕更新时，设置`ResetLogoStatus` = `true` 。



## 其他选项

- 【BGRT.aml】

  如果因“VT-d”问题而必须禁用`DMAR.aml`，设置`Kernel\Quirks\DisableIoMapper` = `true` 。

  `注`：这是BIOS禁用`VT-d`以及ACPI表单`Drop DMAR`的首选项。

