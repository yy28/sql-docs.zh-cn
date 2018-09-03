---
title: SetUnattendedExecutionAccount 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetUnattendedExecutionAccount method
ms.assetid: 1ba6be6f-b05c-4ea0-af98-cd0780290b70
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 58a11122d53c080c0dae57bef722997a0656300e
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43269888"
---
# <a name="configurationsetting-method---setunattendedexecutionaccount"></a>ConfigurationSetting 方法 - SetUnattendedExecutionAccount
  指定用于执行无人参与报表的帐户。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetUnattendedExecutionAccount(UserName as String, _  
    Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetUnattendedExecutionAccount (string UserName,   
    string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *UserName*  
 用于无人参与执行的 Windows 帐户。  
  
 *密码*  
 指定帐户的密码。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 SetUnattendedExecutionAccount 方法不验证报表服务器是否可以指定用户身份登录。  
  
 不能使用 SetUnattendedExecutionAccount 方法在报表服务器 Windows 服务的上下文中运行无人参与的执行。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
