---
title: RSWindowsExtendedProtectionLevel 属性 (WMI MSReportServer_ConfigurationSetting) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f30e5d2399c643e4bc3be5ade3789280dba610f6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66097010"
---
# <a name="rswindowsextendedprotectionlevel-property-wmi-msreportserverconfigurationsetting"></a>RSWindowsExtendedProtectionLevel 属性 (WMI MSReportServer_ConfigurationSetting)
  返回一个字符串值，该值指示配置报表服务器所支持的保护级别。 该属性为只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>备注  
 返回一个字符串值，该值指示配置报表服务器所支持的保护级别。 如果 WMI 提供程序连接到的报表服务器不支持扩展保护，则返回“”（空字符串）。 下表显示有效值：  
  
 `"Off" | "Allow" | "Require"`  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>请参阅  
 [RSWindowsExtendedProtectionScenario 属性 (WMI MSReportServer_ConfigurationSetting)](rswindowsextendedprotectionscenario-property.md)   
 [SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting Services 针对验证的扩展保护](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer 配置文件](../report-server/rsreportserver-config-configuration-file.md)  
  
  
