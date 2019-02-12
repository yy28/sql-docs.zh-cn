---
title: IsSharePointIntegrated 属性 (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 96c8db6fa6d21c0354047061d708250861f0b0c4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016678"
---
# <a name="issharepointintegrated-property-wmi"></a>IsSharePointIntegrated 属性 (WMI)
  指定报表服务器是否处于 SharePoint 集成模式。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，此属性将始终返回 `False`，因为在 SharePoint 模式下，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例为 SharePoint 共享服务，且不受 WMI 提供程序的控制。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>属性值  
 一个 `Boolean` 对象，指示报表服务器是否处于 SharePoint 集成模式。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
