---
title: "RSWindowsExtendedProtectionLevel 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
caps.latest.revision: 6
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 6
---
# RSWindowsExtendedProtectionLevel 属性 (WMI MSReportServer_ConfigurationSetting)
  返回一个字符串值，该值指示配置报表服务器所支持的保护级别。 该属性为只读。  
  
## 语法  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## 注释  
 返回一个字符串值，该值指示配置报表服务器所支持的保护级别。 如果 WMI 提供程序连接到的报表服务器不支持扩展保护，则返回“”（空字符串）。 下表显示有效值：  
  
 `“Off” | “Allow” | “Require”`  
  
## 示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 另请参阅  
 [RSWindowsExtendedProtectionScenario 属性 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario property.md)   
 [SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/setextendedprotectionsettings-method-wmi-msreportserver-configurationsetting.md)   
 [Reporting Services 针对验证的扩展保护](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  