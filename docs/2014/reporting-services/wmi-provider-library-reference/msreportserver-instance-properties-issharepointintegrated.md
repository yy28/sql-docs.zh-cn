---
title: IsSharePointIntegrated 属性 (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 716ff525b322a5722a097ad69dee3e7c3ee97bb6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227097"
---
# <a name="issharepointintegrated-property-wmi-msreportserverinstance"></a>IsSharePointIntegrated 属性 (WMI MSReportServer_Instance)
  指定报表服务器是否处于 SharePoint 集成模式。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，此属性将始终返回 `False`，因为在 SharePoint 模式下，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例为 SharePoint 共享服务，且不受 WMI 提供程序的控制。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>属性值  
 一个 `Boolean` 值，指示报表服务器是否处于 SharePoint 集成模式。  
  
## <a name="requirements"></a>要求  
 **Namespace**：[!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_Instance 成员](msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
  
