---
description: IsSharePointIntegrated 属性 (WMI MSReportServer_Instance)
title: IsSharePointIntegrated 属性 (WMI MSReportServer_Instance) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: abb93d7f4e98009916228e1cb4daf239913d003c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "92255490"
---
# <a name="msreportserver_instance-properties---issharepointintegrated"></a>MSReportServer_Instance 属性 - IsSharePointIntegrated
  指定报表服务器是否处于 SharePoint 集成模式。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]开始，此属性将始终返回 **False** ，因为在 SharePoint 模式下， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例为 SharePoint 共享服务，且不受 WMI 提供程序的控制。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>属性值  
 一个 **Boolean** 值，指示报表服务器是否处于 SharePoint 集成模式。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_Instance 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
