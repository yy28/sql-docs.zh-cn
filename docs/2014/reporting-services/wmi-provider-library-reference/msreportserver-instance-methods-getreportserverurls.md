---
title: GetReportServerUrls 方法 (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9b2963bad73fce65f252ad44ed857f6006978c2f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313189"
---
# <a name="getreportserverurls-method-wmi-msreportserverinstance"></a>GetReportServerUrls 方法 (WMI MSReportServer_Instance)
  返回可用于访问报表服务器和报表管理器的 URL 列表。  
  
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
 一个包含安装的应用程序的数组。 值为`ReportServerWebService`或`ReportManager`。  
  
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
 **Namespace**：[!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
