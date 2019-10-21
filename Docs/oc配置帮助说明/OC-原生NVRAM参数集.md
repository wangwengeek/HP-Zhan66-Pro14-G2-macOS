## OC-原生NVRAM参数集

**一、《引导NVRAM》：7C436110-AB2A-4BBB-A880-FE41995C9F82**

- `boot-args`

  所有kext驱动的启动参数，如：`-v` `keepsyms=1` `-lilubeta` 等。使用方法和clover的`boot`相同。

- `csr-active-config`

  SIP保护掩码，如：67000000。使用方法和clover的`BooterConfig` 、`CsrActiveConfig`相同。

- `prev-lang:kbd`

  以ASCII码设置键盘layout，两种表达格式。

  - 标准格式，如：ru-RU:252（俄文）（ASCII码：`72752D52553A323532`）

  - 简化格式，如：ru:252(俄文)（ASCII码：`72753A323532`）

  - 简体中文，zh-Hans:252（ASCII码：`7A682D48616E733A323532`）
  
  - 默认jian'n'n'n'n'n'n'n'n'n'n'n'n

    注：ru-RU:252是“ABC”键盘layout。所有的键盘layout在AppleKeyboardLayouts-L.dat库文件中。

- `nvda_drv`

  NVIDIA Web驱动控制参数。以ASCII码设置 `31`或 `30`启用或禁用驱动程序。


**二、《系统NVRAM》：4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14**

- `UIScale`

  - 单字节数据，定义用户界面。普通屏幕`UIScale` = `01` ，HIDPI屏幕`UIScale` = `02` 。
  - 关联设置
    - `Misc\Boot\Resolution`—分辨率
    
      - 格式：“长x宽@频率”，或者“长x宽”。如:1920x1080@32，1920x1080。
    
      - 空：不做任何改变。
      - MAX：尝试最大分辨率。
    
    - `UEFI\Quirks\ProvideConsoleGop`
    
      如果固件未提供GOP协议时，设置`UEFI\Quirks\ProvideConsoleGop` = `true` 。
      
      注：如果不清楚可以尝试设置`UEFI\Quirks\ProvideConsoleGop` = `true` 。

- `机型数据`

  机型的所有数据归属**《系统NVRAM》**。如：`PlatformInfo`条目的`Generic`、`DataHub`、`PlatformNVRAM`和`SMBIOS` 。

