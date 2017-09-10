---
title: "新 PowerPivotSystemServiceInstance cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8cde819f27942e78bf67c85356602ad1954420c0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="new-powerpivotsystemserviceinstance-cmdlet"></a>New-PowerPivotSystemServiceInstance cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  向应用程序服务器添加 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务的新实例。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 在你使用 SQL Server 安装程序在本地应用程序服务器上安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 后，New-PowerPivotSystemServiceInstance cmdlet 在场一级预配新的 PowerPivotSystemService 对象。 在每个应用程序服务器上只能设置一个服务实例。  如果该服务已设置，则无法运行此 cmdlet。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-parentservice-powerpivotmidtierservicepipebind"></a>-ParentService \<PowerPivotMidTierServicePipeBind >  
 指定场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务父对象的 GUID。 在此版本中，仅允许一个父对象。 您可以使用 Get-PowerPivotSystemService 返回服务对象或其 GUID。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="-systemserviceinstancename-string"></a>-SystemServiceInstanceName\<字符串 >  
 指定标识此对象的名称。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="provision-switchparameter"></a>设置 [\<SwitchParameter >]  
 使服务在 SharePoint 上可用。 有效值为 $true 或 $false。  
  
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
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 此示例演示该 cmdlet 的最常见的形式。 它在包含场的本地应用程序服务器上注册 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务。  
  
## <a name="example-2"></a>示例 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 此示例命名 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例，但不对实例进行预配。 如果您没有提供名称，则改用默认名称 SQL Server Analysis Services 系统服务实例。 为该服务创建自定义名称是可选的。 您可以命名该服务以便支持测试方案；或者，如果您具有自定义工具或脚本，则可以在以后的步骤中设置该实例。  
  
  
