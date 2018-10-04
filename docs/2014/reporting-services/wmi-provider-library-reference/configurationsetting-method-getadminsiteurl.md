---
title: GetAdminSiteUrl 方法 (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetAdminSiteUrl method
ms.assetid: fbc5bf3c-120c-4aec-a4f2-f5391bd415f6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 68f3811c448fca9921308b520dc6c6ef9a006d5a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098567"
---
# <a name="getadminsiteurl-method-wmi"></a>GetAdminSiteUrl 方法 (WMI)
  获取集成报表服务器的 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]、 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)]、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 场管理中心网站的绝对 URL。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub GetAdminSiteUrl(ByRef AdminSiteUrl as String, _  
ByRef HRESULT as Int32)  
```  
  
```csharp  
public void GetAdminSiteUrl(out string AdminSiteUrl, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *AdminSiteUrl*  
 [out] 一个字符串，包含集成报表服务器的 SharePoint 场管理中心网站的绝对 URL。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 方法](msreportserver-configurationsetting-methods.md)  
  
  
