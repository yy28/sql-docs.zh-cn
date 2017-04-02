---
title: "ReserveURL 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
helpviewer_keywords: 
  - "ReservedURL 方法"
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
caps.latest.revision: 14
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ReserveURL 方法 (WMI MSReportServer_ConfigurationSetting)
  为给定的应用程序添加一个 URL 保留项。  
  
## 语法  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## Parameters  
 *应用程序*  
 为其保留相应 URL 的应用程序的名称。  
  
 *URLString*  
 保留的 URL。  
  
 *lcid*  
 用于返回的错误消息的区域设置。  
  
 *错误*  
 [out] 发生的错误的说明。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## 返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功；错误代码指示调用未成功。  
  
## 注释  
 *UrlString* 不包括虚拟路径名称。 可以使用 [SetVirtualDirectory](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md) 方法实现该目的。  
  
 针对当前 Windows 服务帐户创建 URL 保留项。 更改 Windows 服务帐户需要手动更新所有的 URL 保留项。  
  
 此方法将导致所有应用程序域进行硬回收。 此操作完成后，应用程序域将重新启动。  
  
## 要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  