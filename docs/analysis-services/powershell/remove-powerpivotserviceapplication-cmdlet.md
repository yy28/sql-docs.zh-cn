---
title: 删除 PowerPivotServiceApplication cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 30b7826bf0239ed59b0b94ce624ab1eb212a34fc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="remove-powerpivotserviceapplication-cmdlet"></a>Remove-PowerPivotServiceApplication cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  删除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
Remove-PowerPivotServiceApplication [-Identity <SPGeminiServiceApplicationPipeBind>] [-DeleteAll <switch>] [-RemoveData <switch>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Remove-PowerPivotServiceApplication cmdlet 从场中删除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 使用 DeleteAll 可一次删除所有服务应用程序，或者使用 Identity 参数可删除单个实例。 若要获取实例信息，请运行 Get-PowerPivotServiceApplication 以便返回场中的所有实例。  
  
 使用 RemoveData 参数可以有选择地删除服务应用程序数据库和缓存的文件。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿仍保留在内容库中，但在删除服务应用程序不再起作用。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>标识\<SPGeminiServiceApplicationPipeBind >  
 指定场中单个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序的 GUID。 如果您要仅删除一个应用程序，保持其他服务应用程序不变，则必须指定 GUID。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="-confirm-switch"></a>确认\<切换 >  
 在执行命令前提示您进行确认。 默认情况下将启用该值。 若要在命令中跳过确认响应，请在命令中指定 Confirm:$false。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-deleteall-switch"></a>-DeleteAll\<切换 >  
 删除所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序，但不删除服务应用程序数据库，也不删除场中的服务实例对象。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 引擎服务对象保持实例化，但无法使用。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-removedata-switch"></a>-RemoveData\<切换 >  
 删除包含数据刷新计划、工作簿使用情况数据、用于跟踪加载的数据库的实例映射和其他内部数据的服务应用程序数据库。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
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
C:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop  
```  
  
 此示例将删除单个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序，但不会删除其数据库或缓存。 如果您没有指定标识，系统将会提示您提供一个标识。  
  
## <a name="example-2"></a>示例 2  
  
```  
C:\PS>Remove-PowerPivotServiceApplication -DeleteAll  
```  
  
 此示例删除场中的所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 数据库和缓存不会被删除。  
  
## <a name="example-3"></a>示例 3  
  
```  
CC:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop -RemoveData  
```  
  
 此示例将删除单个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序及其数据库和缓存文件。  
  
  
