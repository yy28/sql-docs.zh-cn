---
title: SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0583632b9c9b8548e16b7a74718b48cad8066ced
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098042"
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
  
 `"Off | Allow | Require"`  
  
 *ExtendedProtectionScenario*  
 设置 RSReportserver.config 文件中的 RSWindowsExtendedProtectionScenario。 必需值不区分大小写。  
  
 下表显示有效值：  
  
 `"Any" | "Proxy" | "Direct"`  
  
## <a name="remarks"></a>备注  
 当 RSReportServer.config 文件中的 AuthenticationTypes 包括 RSWindowNTLM、RSWindowsNegotiate 或 RSWindowsKerberos 时，应用 RSWindowsExtendedProtectionLevel 和 RSWindowsExtendedProtectionScenario 属性。 设置这些属性将影响用户和客户端软件如何在报表服务器上进行身份验证。 建议你在将 ExtendedProtectionLevel 设置为 `Allow` 或 `Require` 前阅读有关扩展保护的文档。  
  
 要设置 ExtendedProtectionLevel，用户必须是报表服务器上 BUILTIN\Administrators 组的成员。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [RSWindowsExtendedProtectionScenario 属性 (WMI MSReportServer_ConfigurationSetting)](rswindowsextendedprotectionscenario-property.md)   
 [RSWindowsExtendedProtectionLevel 属性 (WMI MSReportServer_ConfigurationSetting)](rswindowsextendedprotectionlevel-property.md)   
 [Reporting Services 针对验证的扩展保护](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [RSReportServer 配置文件](../report-server/rsreportserver-config-configuration-file.md)  
  
  
