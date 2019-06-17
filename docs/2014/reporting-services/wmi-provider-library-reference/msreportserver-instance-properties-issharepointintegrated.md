---
title: IsSharePointIntegrated 属性 (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 95e7bade956c791feceddc32f2a0423c331fe77f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097113"
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
 **命名空间:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_Instance 成员](msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
  
