---
title: RSWindowsExtendedProtectionLevel 属性 (WMI MSReportServer_ConfigurationSetting) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
caps.latest.revision: 5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fb0fe7d3c4e7ab433128d774d79a69fd0cb13b03
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268183"
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
  
## <a name="remarks"></a>Remarks  
 返回一个字符串值，该值指示配置报表服务器所支持的保护级别。 如果 WMI 提供程序连接到的报表服务器不支持扩展保护，则返回“”（空字符串）。 下表显示有效值：  
  
 `“Off” | “Allow” | “Require”`  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>请参阅  
 [RSWindowsExtendedProtectionScenario 属性&#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionscenario-property.md)   
 [SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting Services 针对验证的扩展保护](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer 配置文件](../report-server/rsreportserver-config-configuration-file.md)  
  
  
