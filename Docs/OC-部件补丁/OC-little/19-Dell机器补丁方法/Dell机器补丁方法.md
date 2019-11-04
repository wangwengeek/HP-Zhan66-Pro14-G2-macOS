## Dell机器补丁方法

#### 确认DSDT中有以下device名称、Method名称

- EC控制器：ECDV

- 盖子设备：LID0

- Method：BTNV

- Method：OSID

  **注1**：有以上名称的机器，按下列方法组合补丁。
  
  **注2**：无以上名称的机器，请参考OC-部件补丁。
  
  

## 补丁组合

- 公用补丁
- Fn+Insert按键补丁
- 亮度快捷键补丁或 键盘映射（二选一）
- 系统补丁（三选一）



## 公用补丁

- ***SSDT-EC***  ——见《仿冒EC》

- ***SSDT-ALS0*** ——见本章

- ***SSDT-MCHC***  ——见《添加丢失的部件》

- ***SSDT-SBUS***  ——见《SBUS(SMBU)补丁》

- ***SSDT-PLUG-xxx***  ——见《注入X86》

- ***SSDT-PNLF-xxx***  ——见《OC-PNLF注入方法》

- ***SSDT-GPRW***  ——见《0D6D补丁》

  更名：

  ```
  // In config ACPI, GPRW to XPRW
  // Find:     47505257 02
  // Replace:  58505257 02
  ```

  

## Fn+Insert按键补丁

- ***SSDT-PTSWAK***，见《PTSWAK综合补丁和扩展补丁》

  更名：

  ```
  // In config ACPI, _PTS to ZPTS(1,N)
  // Find:     5F50545301
  // Replace:  5A50545301
  // 或者 
  // In config ACPI, _PTS to ZPTS(1,S)
  // Find:     5F50545309
  // Replace:  5A50545309
  ```

  以及：

  ```
  // In config ACPI, _WAK to ZWAK(1,N)
  // Find:     5F57414B01
  // Replace:  5A57414B01
  // 或者
  // In config ACPI, _WAK to ZWAK(1,S)
  // Find:     5F57414B09
  // Replace:  5A57414B09
  ```

- ***SSDT-EXT4-WakeScreen***，见《PTSWAK综合补丁和扩展补丁》

- ***SSDT-LIDpatch***，见《PNP0C0E睡眠修正方法》

  更名：

  ```
  // In config ACPI, _LID to XLID
  // Find:     5F4C4944 00
  // Replace:  584C4944 00
  ```

- ***SSDT-FnInsert_BTNV-dell***，见《PNP0C0E睡眠修正方法》

  更名：

  ```
  // In config ACPI, BTNV to XTNV(dell-Fn+Insert)
  // Find:     42 54 4E 56 02
  // Replace:  58 54 4E 56 02
  ```

  

## 亮度快捷键补丁或键盘映射（二选一）

- ***SSDT-BKeyBRT6-Dell***，见本章

  更名：

  ```
  // In config ACPI, BRT6 to XRT6(dell)
  // Find:     42 52 54 36 02 A0 0B 93
  // Replace:  58 52 54 36 02 A0 0B 93
  ```

- ***键盘映射***，见《PS2键盘映射@OC-xlivans》



## 系统补丁方法一：win7

- ***SSDT-OC-XOSI***，见《操作系统补丁》。补丁内自行设定“Windows 2009”

  - 更名：

  - ```
    // In config ACPI, OSID to XSID
    // Find:     4F534944
    // Replace:  58534944
    //
    // In config ACPI, _OSI to XOSI
    // Find:     5F4F5349
    // Replace:  584F5349
    ```

- ***I2C补丁***

  定制。参考《OCI2C-TPXX补丁方法》

## 系统补丁方法二：win10+

- ***SSDT-OC-XOSI***，见《操作系统补丁》。补丁内自行设定“Windows 2015”或者其他值

  - 更名：

    ```
    // In config ACPI, OSID to XSID
    // Find:     4F534944
    // Replace:  58534944
    //
    // In config ACPI, _OSI to XOSI
    // Find:     5F4F5349
    // Replace:  584F5349
    ```

- ***SSDT-OCWork-dell***，见本章

  使呼吸灯闪烁。

## 系统补丁方法三：单系统

- ***I2C补丁***

  定制。参考《OCI2C-TPXX补丁方法》

- ***SSDT-OCWork-dell***，见本章

  使呼吸灯闪烁。
