---
description: ListReservedURLs 方法 (WMI MSReportServer_ConfigurationSetting)
title: ListReservedURLs 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListReservedURLs method
ms.assetid: 32335af1-5eae-4420-a0ef-b1e8a3267166
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e19d6bf8c8f437f032edd9ad7a26b94f93a7ea7f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454479"
---
# <a name="configurationsetting-method---listreservedurls"></a>ConfigurationSetting 方法 - ListReservedURLs
  列出为报表服务器上所有应用程序保留的 URL。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub ListReservedUrls(ByRef Application() as String, ByRef UrlString() as String, _  
    ByRef Account() as String, ByRef AccountSID() as String, _  
    ByRef length() as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListReservedUrls(out string[] Application, out string[] UrlString,  
        out string[] Account, out string[] AccountSID,  
        out int[] Length, out int[] HRESULT);  
```  
  
## <a name="parameters"></a>参数  
 *Application[]*  
 [out] 具有 URL 预留的应用程序。  
  
 *UrlString[]*  
 [out] 已保留的 URL。  
  
 *Account[]*  
 [out] 与 URL 预留的帐户关联的帐户名。  
  
 *AccountSID[]*  
 [out] 与 URL 预留的帐户关联的帐户 SID。  
  
 *长度*  
 [out] 该方法返回的数组长度。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功；错误代码指示调用未成功。  
  
## <a name="remarks"></a>备注  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
