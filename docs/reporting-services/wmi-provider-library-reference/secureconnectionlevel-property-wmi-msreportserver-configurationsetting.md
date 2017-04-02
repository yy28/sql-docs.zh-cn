---
title: "SecureConnectionLevel 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "SecureConnectionLevel"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "SecureConnectionLevel 属性"
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
caps.latest.revision: 19
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# SecureConnectionLevel 属性 (WMI MSReportServer_ConfigurationSetting)
  返回 RSReportServer.config 文件中指定的安全连接级别。 只读。  
  
## 语法  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## 属性值  
 表示安全连接级别的 **Integer** 值。 返回值表示是否配置 SSL。 值大于或等于 1 表示打开了 SSL。 值为 0 表示关闭了 SSL。  
  
## 示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  