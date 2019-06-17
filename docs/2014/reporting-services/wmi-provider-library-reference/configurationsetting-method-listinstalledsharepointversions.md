---
title: ListInstalledSharePointVersions 方法 (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListInstalledSharePointVersions method
ms.assetid: 8f0a5e9f-23f1-41e5-9a90-dfec19ef1df7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b67f20c8d20e21ac7af197d4d8ec7fe780a8fd83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098343"
---
# <a name="listinstalledsharepointversions-method-wmi"></a>ListInstalledSharePointVersions 方法 (WMI)
  返回一组标记，表示与报表服务器安装在同一台计算机上的 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub ListInstalledSharePointVersions(ByRef VersionTokens() _  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] VersionTokens,   
    out Int32 Length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *VersionTokens[]*  
 [out] 一个包含表示 SharePoint 产品或技术的版本的标记的数组，该版本与安装的报表服务器兼容。  
  
 *长度*  
 [out] 版本标记数组的长度。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 返回的每个标记都表示一个与当前安装的报表服务器兼容的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 或 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 版本。 如果某个 SharePoint 特定版本兼容 SharePoint 的早期版本，则会返回每个 SharePoint 兼容版本的标记。  
  
 下表说明了返回的 SharePoint 标记。  
  
|**版本标记**|**说明**|  
|------------------------|---------------------|  
|WSS_V2_Compatible|安装的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 系统与 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0 兼容。|  
|WSS_V3_Compatible|安装的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 系统与 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 兼容。|  
|WSS_V4_Compatible|安装的 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 系统与 Office 14 兼容。|  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
