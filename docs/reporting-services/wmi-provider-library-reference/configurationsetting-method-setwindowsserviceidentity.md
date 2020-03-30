---
title: SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b12b21fe8e51f8c03bf01efd7df63053c528781
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "65570914"
---
# <a name="configurationsetting-method---setwindowsserviceidentity"></a>ConfigurationSetting 方法 - SetWindowsServiceIdentity
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
  
## <a name="parameters"></a>parameters  
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
 UseBuiltInAccount 参数设置为 true 并且报表服务器在 Microsoft  *或 Windows XP 上运行时，将忽略 Name、Domain 和 Password 参数的值，并且使用本地系统帐户*  [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]    。  
  
 UseBuiltInAccount 参数设置为 true 并且报表服务器在 Windows Server 2003 上运行时，将忽略 Domain 和 Password 属性，并且名称字段必须包含“Builtin\NetworkService”、“Builtin\System”或“Builtin\LocalService”     。  
  
 SetWindowsServiceIdentity 方法可对报表服务器安装目录中的文件和文件夹设置文件权限。  
  
 *Account* 参数中指定的帐户要求 Windows 中的 **LogonAsService** 权限。 该方法可将此权限授予指定的帐户。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
