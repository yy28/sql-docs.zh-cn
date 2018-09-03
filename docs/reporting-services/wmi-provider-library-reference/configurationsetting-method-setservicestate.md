---
title: SetServiceState 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f4eeee0ba266c99fbb74b926d7fcf258843ad302
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274434"
---
# <a name="configurationsetting-method---setservicestate"></a>ConfigurationSetting 方法 - SetServiceState
  打开和关闭报表服务器 Windows 服务和 Web 服务。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetServiceState(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *EnableWindowsService*  
 指示 Windows 服务状态的 **Boolean** 值。 如果值为 **true** ，则会启动报表服务器 Windows 服务；如果值为 **false** ，则会停止该 Windows 服务。  
  
 *EnableWebService*  
 指示 **Web 服务状态的** Boolean [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 值。 如果值为 **true** ，则会启动报表服务器 Web 服务；如果值为 **false** ，则会停止该 Web 服务。  
  
 *EnableReportManager*  
 指示所需的报表管理器状态的 **Boolean** 值。
 
 > [!NOTE] 
 > 从 SQL Server 2016 Reporting Services 累积更新 2 开始已弃用此设置。 将始终启用 Web 门户。 将忽略值。
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
