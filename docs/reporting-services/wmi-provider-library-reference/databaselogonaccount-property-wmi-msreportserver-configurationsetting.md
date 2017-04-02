---
title: "DatabaseLogonAccount 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "DatabaseLogonAccount"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "DatabaseLogonAccount 属性"
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
caps.latest.revision: 24
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# DatabaseLogonAccount 属性 (WMI MSReportServer_ConfigurationSetting)
  指定报表服务器连接到报表服务器数据库时使用的登录帐户。 只读。  
  
## 语法  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## 属性值  
 表示登录帐户名的 **String** 对象。  
  
## 示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## 注释  
 此属性的有效值将因 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md) 属性的值而异。  
  
 如果 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md) 属性设置为 **2 (Service)**，则将忽略此属性。  
  
## 要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  