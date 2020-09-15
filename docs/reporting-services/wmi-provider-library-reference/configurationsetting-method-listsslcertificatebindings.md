---
description: ListSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)
title: ListSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bdd6cc584b43ee72c43eec7abc1ad50398f1b2eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423171"
---
# <a name="configurationsetting-method---listsslcertificatebindings"></a>ConfigurationSetting 方法 - ListSSLCertificateBindings
  返回计算机上已安装的 TLS/SSL 证书的列表。  
  
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
  
## <a name="parameters"></a>参数  
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
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
