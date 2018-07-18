---
title: ListReportServersInDatabase 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: dfb91a3cc4326f1fa52661002b2a9d8c69c6e52a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33030174"
---
# <a name="configurationsetting-method---listreportserversindatabase"></a>ConfigurationSetting 方法 - ListReportServersInDatabase
  返回报表服务器数据库中存在的报表服务器安装列表，无论这些安装是否具有访问安全信息的权限都同样如此。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parameters  
 *MachineNames[]*  
 [out] 一个数组，包含数据库中存在的各个报表服务器安装的计算机名称。  
  
 *InstanceNames[]*  
 [out] 一个数组，包含数据库中存在的各个报表服务器安装的实例名称。  
  
 *InstallationIDs[]*  
 [out] 一个数组，包含数据库中存在的各个报表服务器安装的安装 ID。  
  
 *IsInitialized[]*  
 [out] 一个数组，包含数据库中存在的各个报表服务器安装的初始化状态。  
  
 *长度*  
 [out] 该方法返回的数组长度。 所有返回数组的长度都相同。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
 *ExtendedErrors[]*  
 [out] 一个字符串数组，包含此调用返回的其他错误。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 ListReportServersInDatabase 用于列出报表服务器数据库中存在的报表服务器安装（无论这些安装是否具有访问安全信息的权限），并返回一组包含每一安装相关信息的匹配数组。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
