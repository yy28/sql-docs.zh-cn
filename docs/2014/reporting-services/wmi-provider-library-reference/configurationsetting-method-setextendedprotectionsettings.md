---
title: SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 81b0ea8c7142f33ef9fc91622d899e54f21fe756
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076208"
---
# <a name="setextendedprotectionsettings-method-wmi-msreportserverconfigurationsetting"></a>SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)
  SetExtendedProtectionSettings 方法用于设置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置文件 RSReportServer.config 中的 RSWindowsExtendedProtectionLevel 和 RSWindowsExtendedProtectionScenario 属性。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetExtendedProtectionSettings( _  
        ByVal ExtendedProtectionLevel As String, _  
        ByVal ExtendedProtectionScenario As String, _  
        ByRef Warnings() As String, _  
        ByRef Length As Int32, _  
        ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetExtendedProtectionSettings(  
            string ExtendedProtectionLevel,  
            string ExtendedProtectionScenario,  
            out string[] Warnings,  
            out Int32 Length,  
            out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *ExtendedProtectionLevel*  
 设置 RSRreportserver.config 文件中的 RSWindowsExtendedProtectionLevel。 必需值不区分大小写。  
  
 下表显示有效值：  
  
 `”Off | Allow | Require”`  
  
 *ExtendedProtectionScenario*  
 设置 RSReportserver.config 文件中的 RSWindowsExtendedProtectionScenario。 必需值不区分大小写。  
  
 下表显示有效值：  
  
 `”Any” | “Proxy” | “Direct”`  
  
## <a name="remarks"></a>备注  
 当 RSReportServer.config 文件中的 AuthenticationTypes 包括 RSWindowNTLM、RSWindowsNegotiate 或 RSWindowsKerberos 时，应用 RSWindowsExtendedProtectionLevel 和 RSWindowsExtendedProtectionScenario 属性。 设置这些属性将影响用户和客户端软件如何在报表服务器上进行身份验证。 建议您阅读有关在将 ExtendedProtectionLevel 设置为之前的扩展保护的文档`Allow`或`Require`。  
  
 要设置 ExtendedProtectionLevel，用户必须是报表服务器上 BUILTIN\Administrators 组的成员。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [RSWindowsExtendedProtectionScenario 属性&#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionscenario-property.md)   
 [RSWindowsExtendedProtectionLevel 属性&#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Reporting Services 针对验证的扩展保护](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer 配置文件](../report-server/rsreportserver-config-configuration-file.md)  
  
  
