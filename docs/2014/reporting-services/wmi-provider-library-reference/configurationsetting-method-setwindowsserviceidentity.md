---
title: SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dc59e8a963f39a3686e7d7cb02cd2e2b17a39783
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947063"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserverconfigurationsetting"></a>SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting)
  将报表服务器 Windows 服务作为指定的 Windows 用户运行，并授予此帐户足够的文件系统权限以允许操作报表服务器。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *UseBuiltInAccount*  
 指示指定的帐户是否是内置 Windows 帐户。  
  
 *帐户*  
 要用于运行 Windows 服务的 Windows 帐户，格式为“DOMAIN\alias”。  
  
 *密码*  
 帐户的密码。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 当*UseBuiltInAccount*参数设置为`true`并且报表服务器正在运行 microsoft[!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]或 Windows XP，则*名称*，*域*，并*密码*参数将被忽略，并使用本地系统帐户。  
  
 当*UseBuiltInAccount*参数设置为`true`并且报表服务器正在运行 Windows Server 2003 上*域*并*密码*属性被忽略，并且名称字段必须包含"Builtin\NetworkService"或"Builtin\System"或"Builtin\LocalService"。  
  
 SetWindowsServiceIdentity 方法可对报表服务器安装目录中的文件和文件夹设置文件权限。  
  
 中指定的帐户*帐户*参数需要`LogonAsService`Windows 中的权限。 该方法可将此权限授予指定的帐户。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
