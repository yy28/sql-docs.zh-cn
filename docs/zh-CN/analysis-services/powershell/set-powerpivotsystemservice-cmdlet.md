---
title: 集 PowerPivotSystemService cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00f080d09fd433d22ecf0e5eebeb84e7fc6394d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="set-powerpivotsystemservice-cmdlet"></a>Set-PowerPivotSystemService cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  设置场级别 PowerPivotSystemService 对象的全局属性。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
Set-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [-UpdateAssemblyInformation <switch>] [-WorkbookUpgradeOnDataRefresh <boolean>] [-DirectTCPConnections <boolean>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Set-PowerPivotSystemService cmdlet 更新场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务父对象的属性。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>-Identity \<PowerPivotMidTierServicePipeBind>  
 指定要更新其属性的父对象。 该值必须是一个有效的 GUID，用于唯一标识场中的对象。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="-updateassemblyinformation-switch"></a>-UpdateAssemblyInformation\<切换 >  
 仅用于升级目的。 如果在场中部署的程序集版本不同于在 SharePoint 配置数据库中存储的版本，则可以运行此 cmdlet 以便更新配置数据库中的程序集信息。 程序集版本信息在全局程序集中存储的 Microsoft.AnalysisServices.SharePoint.Integration.dll 的文件属性中提供。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-workbookupgradeondatarefresh-boolean"></a>-WorkbookUpgradeOnDataRefresh\<布尔 >  
 用于在服务器上计划的数据刷新开始时自动升级 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 工作簿。 只有与服务器的当前版本匹配的工作簿才支持数据刷新。 如果启用了此属性，工作簿将自动升级以便数据刷新可以继续进行。 该属性在服务实例级别设置。 您不能为特定的工作簿、库、站点或用户而改变该工作簿。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|2|  
|默认值|false|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-directtcpconnections-boolean"></a>-DirectTCPConnections\<布尔 >  
 指定 Excel Services 将所有查询直接发送到加载了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库的 SQL Server Analysis Services (POWERPIVOT) 的实例，并且跳过用于发送到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库的每个查询请求的 MSOLAP 数据提供程序和管道传输。  
  
 设置此参数可通过更高效地建立与已加载数据库的连接，改进 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查询的性能和可伸缩性。 请注意，此参数不会更改分配初始加载请求的行为方式。 用于在场中的多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 实例之间分配数据库加载请求的其他参数（例如 –RoundRobinAllocation 和 –HealthBasedAllocation）不会受到影响，因为 –DirectTCPConnections 仅应用于在加载数据库后发出的查询。  
  
 对于包含在单独的应用程序服务器上分别运行的 Excel Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的场拓扑结构，必须在防火墙中打开一个端口，以便确保请求到达 SQL Server Analysis Services (POWERPIVOT) 实例。 有关如何为 Analysis Services 的命名实例启用入站连接的说明，请参阅 [将 Windows 防火墙配置为允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|3|  
|默认值|false|  
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
C:\PS>Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true  
```  
  
 启用以前版本工作簿的自动升级，以便可以继续执行计划的数据刷新。  
  
  
