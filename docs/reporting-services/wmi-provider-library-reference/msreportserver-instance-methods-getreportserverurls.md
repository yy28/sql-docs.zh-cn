---
title: GetReportServerUrls 方法 (WMI MSReportServer_Instance) | Microsoft Docs
ms.date: 06/09/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2b16393c0f89e3199975914f35e2d066d0d5a561
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43276375"
---
# <a name="msreportserverinstance-methods---getreportserverurls"></a>MSReportServer_Instance 方法 - GetReportServerUrls
  返回用户可用于访问报表服务器和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]的 URL 列表。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *ApplicationName[]*  
 一个包含安装的应用程序的数组。 值为 **ReportServerWebService** 或 **ReportServerWebApp**。  
  
 *URLs[]*  
 一个包含已成功注册的 URL 的数组。  
  
 *长度*  
 一个包含返回数组的长度的整数值。  
  
 *HRESULT*  
 一个指示成功或错误代码的值。  
  
## <a name="return-values"></a>返回值  
  
## <a name="remarks"></a>Remarks  
 可通过 InvokeMethod 函数调用由 WMI 管理对象公开的方法。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI 文档中的“Executing Methods on Management Objects”（对管理对象执行方法）。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
