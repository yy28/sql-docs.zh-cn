---
title: "ListIPAddresses 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "ListIPAddresses 方法"
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# ListIPAddresses 方法 (WMI MSReportServer_ConfigurationSetting)
  列出报表服务器计算机的 IP 地址。  
  
## 语法  
  
```vb  
Public Sub ListIPAddresses (ByRef IPAddress() as String, _  
    ByRef IPVersion()as String, ByRef IsDhcpEnabled () as Boolean, _   
    ByRef Length as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListIPAddresses (out string[] IPAddress,   
    out string[] IPVersion, out bool[] isDhcpEnabled, out int length,   
    out int HRESULT);  
```  
  
## Parameters  
 *IPAddress[]*  
 [out] 计算机的 IP 地址列表。  
  
 *IPVersion[]*  
 [out] IP 地址的版本。  
  
 *IsDhcpEnabled[]*  
 [out] 指示 IP 地址是否已启用 DHCP。  
  
 *长度*  
 [out] 该方法返回的数组长度。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## 返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功；错误代码指示调用未成功。  
  
## 注释  
 *IPVersion* 字符串为 V4、V6。  
  
 如果 *IsDhcpEnabled* 为 **True**， *IPAddress* 将是动态的。 不应用于 SSL 绑定。  
  
## 要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## 另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  