## OC机型设置

1. 概述

   ​	OC机型设置于`config\PlatformInfo`。按设置内容划分为简单设置和完全设置。

   - 简单设置，设置`Automatic=true`，填写`Generic`内容。

   - 完全设置，设置`Automatic=false`，填写`DataHub`、`PlatformNVRAM`、`SMBIOS`内容。

     无论简单设置还是完全设置，在样本文件的基础上修改部分内容即可。

     ***`警告`***：不可以用`OpenCore Configurator.app`编辑`config.plist`。但可以使用它生成的机型数据。

2. 简单设置

   - Generic
     - `SystemProductName`，如：MacBookPro14,2 

3. 完全设置

   - DataHub
     - `BoardProduct`，如：Mac-CAD6701F7CEA0921
     - `SystemProductName`，如：MacBookPro14,2 
   - PlatformNVRAM
     - `BID`，如：Mac-CAD6701F7CEA0921
     - `FirmwareFeatures`，如：37E10FFC 00000000
     - `FirmwareFeaturesMask`，如：3FFF1FFF 00000000
   - SMBIOS
     - `BoardProduct`，如：Mac-CAD6701F7CEA0921
     - `BoardVersion`，如：MacBookPro14,2 
     - `ChassisVersion`，如：Mac-CAD6701F7CEA0921
     - `FirmwareFeatures`，如：37E10FFC 00000000
     - `FirmwareFeaturesMask`，如：3FFF1FFF 00000000
     - `SystemProductName`，如：MacBookPro14,2 
     - `SystemSKUNumber`，如：Mac-CAD6701F7CEA0921
   

