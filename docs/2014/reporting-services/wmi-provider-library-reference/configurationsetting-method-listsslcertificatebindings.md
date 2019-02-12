---
title: ListSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9802176b5f5c82ba60a4e47d85445b54eaa1a5f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031618"
---
# <a name="listsslcertificatebindings-method-wmi-msreportserverconfigurationsetting"></a>ListSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)
  返回计算机上已安装的 SSL 证书的列表。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub ListSSLCertificateBindings(ByVal LCID As Int32, ByRef Application() As String, _  
    ByRef CertificateHash() As String, ByRef IPAddresses() As String, ByRef Port() As Int32, _  
    ByRef Errors() As String, ByRef Length As Int32, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListSSLCertificateBindings(Int32 Lcid, out string[] Application,   
    out string[] CertificateHash,out string[] IPAddress,   
    out Int32[] Port, out string Errors,   
    out Int32 length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *LCID*  
 用于返回的错误消息的区域设置。  
  
 *Application[]*  
 [out] 具有证书绑定的应用程序。  
  
 *CertificateHash[]*  
 [out] 证书的哈希。  
  
 *IPAddress[]*  
 [out] 应用程序的 IP 地址。  
  
 *Port[]*  
 [out] 存储在 rsreportserver.config 中的绑定中的端口号。  
  
 *Errors[]*  
 [out] 发生的错误的说明。  
  
 *长度*  
 [out] 该方法返回的数组长度。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
