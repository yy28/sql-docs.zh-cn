---
title: ListIPAddresses 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListIPAddresses method
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1207c4c9688826b599548477a35ca123b9d39c28
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65579939"
---
# <a name="configurationsetting-method---listipaddresses"></a>ConfigurationSetting 方法 - ListIPAddresses
  列出报表服务器计算机的 IP 地址。  
  
## <a name="syntax"></a>语法  
  
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
  
## <a name="parameters"></a>parameters  
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
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功；错误代码指示调用未成功。  
  
## <a name="remarks"></a>备注  
 *IPVersion* 字符串为 V4、V6。  
  
 如果 *IsDhcpEnabled* 为 **True**， *IPAddress* 将是动态的。 不应用于 SSL 绑定。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
