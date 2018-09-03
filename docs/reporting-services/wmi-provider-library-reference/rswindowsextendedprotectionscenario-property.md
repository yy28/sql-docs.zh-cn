---
title: RSWindowsExtendedProtectionScenario 属性 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aa66222fd6880d9559cdae450a07c53a73c2ccab
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43264879"
---
# <a name="rswindowsextendedprotectionscenario-property"></a>RSWindowsExtendedProtectionScenario 属性
  返回一个字符串值，该值指示报表服务器配置为允许的扩展保护方案。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## <a name="remarks"></a>Remarks  
 返回一个字符串值，该值指示报表服务器配置为允许的扩展保护方案。 如果 WMI 提供程序连接到的报表服务器不支持扩展保护，则返回“”（空字符串）。  
  
 下表显示有效值：  
  
 `”Any | Proxy | Direct”`  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>另请参阅  
 [RSWindowsExtendedProtectionLevel 属性 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Reporting Services 针对验证的扩展保护](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
