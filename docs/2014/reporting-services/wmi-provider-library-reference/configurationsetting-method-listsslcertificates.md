---
title: ListSSLCertificates 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificates method
ms.assetid: 88cd0936-b202-4ab8-90f2-d9c3f66d37f4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a83096e8b1fe3eed9e0df513931b812125955f61
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221717"
---
# <a name="listsslcertificates-method-wmi-msreportserverconfigurationsetting"></a>ListSSLCertificates 方法 (WMI MSReportServer_ConfigurationSetting)
  返回报表服务器计算机上证书的列表。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub CreateSSLCertificateBinding (ByRef CertificateHash() as String, _  
    ByRef CertName() as String, ByRef HostName() as String, ByRef Length as Int32, _   
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListSSLCertificates(out string[] CertificateHash,   
    out string[] CertName, out string[] Hostname, out Int32 length,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *CertificateHash[]*  
 [out] 证书哈希。  
  
 *CertName[]*  
 [out] 证书名称。  
  
 *HostName[]*  
 [out] 证书的主机名。  
  
 *长度*  
 [out] 表示 *CertificateHash*、 *CertName* 和 *HostName* 数组的长度。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功；错误代码指示调用未成功。  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
