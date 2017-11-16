---
title: "Get-powerpivotsystemservice cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 33231250-3880-4d75-936b-d70662a01855
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1b1878ab48daa6c13e633daa62deada76512d3bd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="get-powerpivotsystemservice-cmdlet"></a>Get-PowerPivotSystemService cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  返回场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务对象的全局属性。 

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
Get-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Get-PowerPivotSystemService cmdlet 返回 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务对象的全局属性。 每个场只有一个父对象，但每个场可以有多个在场中各应用程序服务器上运行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例。 父对象显示不会按实例而改变的场级别设置。 如果场中包括多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装，则实例的以逗号分隔的列表将指示在场中有多少个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>标识\<PowerPivotMidTierServicePipeBind >  
 指定要获取的父对象。 该值必须是一个有效的 GUID，用于唯一标识场中的对象。  
  
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
C:\PS>Get-PowerPivotSystemService  
```  
  
 此示例返回父对象的全局属性，并且显示场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务的所有实例共享的属性。  
  
  

