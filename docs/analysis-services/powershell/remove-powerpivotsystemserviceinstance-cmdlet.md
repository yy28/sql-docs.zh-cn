---
title: "删除 PowerPivotSystemServiceInstance cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e44d28106db0c14c293c463d91125b262190350d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Remove-PowerPivotSystemServiceInstance cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  从场中删除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Remove-PowerPivotSystemServiceInstance cmdlet 从场中删除与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务有关的实例信息。 它不会删除程序文件。 若要永久删除程序文件，您必须卸载它们。  
  
 如果删除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务，请确保还运行 Remove-PowerPivotEngineServiceInstance 以便删除关联的 Analysis Services 实例，之后使用 Remove-PowerPivotServiceApplication 删除所有 PowerPivot 服务应用程序。 在这些服务都被删除后，服务应用程序将不再运行。  
  
 若要还原此更改，可以运行 New-PowerPivotSystemServiceInstance -Provision:$true 以便重新启用实例信息。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>标识\<PowerPivotMidTierServiceInstancePipeBind >  
 指定要删除的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例的 GUID。 在安装有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的每个应用程序服务器上只有一个服务实例。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="-deletelocal-switch"></a>-DeleteLocal\<切换 >  
 删除在本地计算机上安装的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例，并且允许你不必指定对象标识即删除实例。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
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
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 此示例演示如何删除在本地应用程序服务器上运行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例。  
  
## <a name="example-2"></a>示例 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 此示例演示如何基于其标识删除特定的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务。  
  
  

