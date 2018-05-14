---
title: Get PowerPivotServiceApplication cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a5ccd05b8c5e947972218a22c0abbc358731ee5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="get-powerpivotserviceapplication-cmdlet"></a>Get-PowerPivotServiceApplication cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  返回一个或多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Get-PowerPivotServiceApplication cmdlet 返回 Identity 参数指定的服务应用程序。 如果未指定任何参数，cmdlet 将返回场中的所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 每个应用程序都由其显示名称、应用程序类型和 GUID 标识。 若要查看 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序的其他属性，请向该 cmdlet 添加 format-list 选项。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>标识\<SPGeminiServiceApplicationPipeBind >  
 指定要获取的服务应用程序。 该值必须是一个有效的 GUID，用于唯一标识场中的对象。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下常用参数：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|无。|  
|输出|无。|  
  
## <a name="example-1"></a>示例 1  
  
```  
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 此示例返回场中的一个或多个服务应用程序。  
  
## <a name="example-2"></a>示例 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 此示例返回 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序的所有属性。  
  
## <a name="example-3"></a>示例 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 此示例返回单个服务应用程序，并且显示其显示名称、应用程序类型和应用程序的 GUID。 如果显示名称太长，它将被截断。 使用 format-list 选项可以查看完整名称。  
  
  
