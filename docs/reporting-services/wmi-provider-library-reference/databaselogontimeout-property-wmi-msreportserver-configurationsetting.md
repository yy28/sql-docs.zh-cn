---
title: "DatabaseLogonTimeout 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "DatabaseLogonTimeout Property"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "DatabaseLogonTimeout 属性"
ms.assetid: 4a65162c-33de-485e-8fd3-2bd6bff8bf8d
caps.latest.revision: 38
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# DatabaseLogonTimeout 属性 (WMI MSReportServer_ConfigurationSetting)
  指定尝试登录到报表服务器数据库失败前等待的秒数。 值 **0** 指示无限期的等待时间。 只读。  
  
## 语法  
  
```vb  
Public Dim DatabaseLogonTimeout As Int32  
```  
  
```csharp  
public Int32 DatabaseLogonTimeout;  
```  
  
## 属性值  
 一个表示秒数的 32 位带符号整数对象。  
  
## 示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  