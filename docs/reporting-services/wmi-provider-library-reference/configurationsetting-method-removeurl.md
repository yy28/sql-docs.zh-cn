---
description: RemoveURL 方法 (WMI MSReportServer_ConfigurationSetting)
title: RemoveURL 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 69112a88d00af4c82e10471addc32eff6d3e7cde
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423151"
---
# <a name="configurationsetting-method---removeurl"></a>ConfigurationSetting 方法 - RemoveURL
  删除为报表服务器保留的 URL。 如果需要删除多个 URL，则必须逐个调用此 API 来完成操作。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>参数  
 *应用程序*  
 要为其删除预留的应用程序的名称。  
  
 *URLString*  
 预留的 URL。  
  
 *lcid*  
 用于返回的错误消息的区域设置。  
  
 *错误*  
 [out] 发生的错误的说明。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功；错误代码指示调用未成功。  
  
## <a name="remarks"></a>备注  
 UrlString 不包括虚拟目录名 - [SetVirtualDirectory 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) 是为实现该目的所提供的方法  。  
  
 在调用 [ReserveURL](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md) 方法之前，必须为 *Application* 参数的 VirtualDirectory 配置属性提供一个值。 使用 [SetVirtualDirectory 方法 (WMI MSReportServer_ConfigurationSetting )](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) 方法设置 VirtualDirectory 属性。  
  
 如果 TLS/SSL 证书是由 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 预配，但没有其他 URL 需要它，它就会被删除。  
  
 此方法会导致所有非配置应用程序域在执行此操作时进行硬回收并停止；应用程序域将在此操作完成后重新启动。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
