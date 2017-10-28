---
title: "CreateSSLCertificateBinding 方法 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1d9a797922bc8d7b39e7b7c43897d4ae5ee5bd28
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---createsslcertificatebinding"></a>ConfigurationSetting 方法-CreateSSLCertificateBinding
  创建 SSL 证书绑定。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *应用程序*  
 应为其创建证书绑定的应用程序的名称。  
  
 *CertificateHash*  
 证书的哈希。  
  
 *IPAddress*  
 应用程序的 IP 地址。  
  
 *端口*  
 与该绑定关联的 SSL 端口。  
  
 *Lcid*  
 用于返回的错误消息的区域设置。  
  
 *错误*  
 [out] 发生的错误的说明。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功；错误代码指示调用未成功。  
  
## <a name="remarks"></a>注释  
 此方法将向 rsreportserver.config 中为该应用程序添加一个绑定。 如果某个绑定在 HTTP.SYS 中不存在，则会在其中创建它。  
  
 在创建绑定之前，该方法调用会检查指定应用程序的 Url 保留项，以确定 SSL 证书绑定是否有效。  
  
 如果验证到存在以下情况，则会导致错误：  
  
1.  证书不存在。  
  
2.  指定的 IPAddress 与此计算机的 IPAddress 不对应。  
  
3.  指定的 IPAddress 为 DHCP IPAddress（定期更改）– 请改用通配符 IP 地址 (0.0.0.0)。  
  
4.  指定的 IPAddress 与某个 URL 保留项的 IP 地址不匹配，并且没有通配符或主机名 URL 保留项。  
  
5.  指定某个主机名的 URL 保留项已存在，但是该主机名与证书主机名不匹配。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

