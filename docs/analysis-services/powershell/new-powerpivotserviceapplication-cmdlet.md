---
title: "新 PowerPivotServiceApplication cmdlet |Microsoft 文档"
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
ms.assetid: 7bb2a2d2-04c8-43d4-a0fc-e8339ea22138
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a574a1159d984e59a7a8ee5ff58ae63f16199b0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="new-powerpivotserviceapplication-cmdlet"></a>New-PowerPivotServiceApplication cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  创建新的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
New-PowerPivotServiceApplication [-ServiceApplicationName] <string> [-DatabaseServerName] <string> [-DatabaseName] <string> [-AddToDefaultProxyGroup <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 New-PowerPivotServiceApplication cmdlet 在场中创建新的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 您必须定义至少一个 PowerPivot 服务应用程序，并且它必须是默认代理服务组的成员。 如果您需要更改属性或配置设置，还可以创建其他的服务应用程序。 必须向附加服务应用程序分配自定义服务连接组的成员身份。 只能有一个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序可以是默认代理组的成员。  
  
 使用默认配置创建新的服务应用程序。 若要自定义配置属性，可使用 Set-PowerPivotServiceApplication cmdlet。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-serviceapplicationname-string"></a>-ServiceApplicationName\<字符串 >  
 设置服务应用程序的显示名称。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-databaseservername-string"></a>-DatabaseServerName\<字符串 >  
 指定承载应用程序数据库的 SQL Server 关系数据库引擎实例。 默认情况下，您可以使用场的数据库服务器，或者可以选择对其具有创建数据库权限的另一个数据库服务器。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-databasename-string"></a>-DatabaseName\<字符串 >  
 指定存储应用程序数据的 SQL Server 关系数据库的名称。 请确保指定与应用程序相对应的名称，以便您可以更轻松地标识其用途。 你可以创建新的数据库，或者为你创建的新的应用程序指定现有的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|2|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-addtodefaultproxygroup-switch"></a>-AddToDefaultProxyGroup\<切换 >  
 在默认服务连接组中创建 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务连接。 此组中的成员身份确定 Web 应用程序和服务应用程序之间的关联。 订阅默认服务连接组的所有 Web 应用程序都可以使用你添加到该组的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 尽管你可以在一个场中具有多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序，但只有一个服务应用程序可以是默认服务连接组的成员。  
  
 如果你已经有一个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序是默认代理组的成员，则必须为你正在创建的新应用程序设置 AddToDefautlProxyGroup:$false。 您将需要向自定义服务连接组添加这个新的服务应用程序。  您可以将内置的 SharePoint cmdlet 用于此目的。  Get-SPServiceApplicationProxyGroup 返回在场中定义的服务连接组的列表。  
  
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
C:\PS>New-PowerPivotServiceApplication -ServiceApplicationName "PowerPivot Service Application" -DatabaseServerName "AdvWorks-SRV01\PowerPivot" -DatabaseName "PowerPivotServiceApp1" -AddtoDefaultProxyGroup:$true  
```  
  
 该示例创建一个新的服务应用程序。 该服务应用程序数据库是在名为 AdvWorks-SRV01 的一个数据库服务器上创建的，该数据库服务器已作为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 命名实例安装，它具有许多 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装所共有的配置。 您必须对该 SQL Server 实例具有 dbcreator 权限，才能创建该数据库。 您必须是 SharePoint 配置数据库上的 db_owner。 因为这是场中的第一个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序，所以它必须是默认代理组的成员。  
  
  

