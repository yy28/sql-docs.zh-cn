---
title: MSSQLSERVER_916 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 916 (Database Engine error)
ms.assetid: 73eb6581-99fe-49a5-9b42-e239d7ffe27f
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 69490614063e878043c59bce1bc7836f813eb517
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver916"></a>MSSQLSERVER_916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|916|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NOTUSER|  
|消息正文|服务器主体 "%.*ls" 无法在当前安全上下文下访问数据库 "%.\*ls"。|  
  
## <a name="explanation"></a>解释  
该登录名没有足够的权限，无法连接到命名的数据库。 可以连接到此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例但在数据库中没有特定权限的登录名将获得 guest 用户的权限。 这是一项安全举措，为了防止一个数据库中的用户连接到他们没有权限的其他数据库。 当 guest 用户没有 CONNECT 权限而无法连接到命名数据库并且未设置可信属性时，会出现此错误消息。 当 guest 用户没有 CONNECT 权限而无法连接到命名数据库时，会出现此错误消息。  
  
当对 msdb 数据库的 CONNECT 权限被拒绝或撤消时，如果对象资源管理器尝试显示每个数据库的“基于策略的管理”状态，则 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可能收到此错误。 对象资源管理器使用当前登录名的权限查询 msdb 数据库以获取此信息，这会导致错误。 还会出现以下错误信息：  
  
无法为此请求检索数据。 (Microsoft.SqlServer.Management.Sdk.Sfc)  
  
## <a name="user-action"></a>用户操作  
  
> [!WARNING]  
> 在采取此安全措施前，请确保您明确理解用户是在不同的数据库中验证身份的。 下面的方法可能会允许在一个数据库中具有权限的用户连接到其他数据库，这可能会向恶意用户公开数据。 在启用包含数据库后，以下步骤将允许一个数据库中的数据库所有者授予对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的其他数据库的访问权限。  
  
可以按以下方式之一连接到数据库：  
  
-   向特定登录名授予针对命名数据库的访问权限。 下面的示例向登录名 `Adventure-Works\Larry` 授予针对 `msdb` 数据库的访问权限。  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO [Adventure-Works\Larry] ;  
  
-   向 guest 用户授予针对在错误消息中指定的数据库的 CONNECT 权限。 以下示例授予用户 `CONNECT` 对 `msdb` 数据库的 `guest` 权限。  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO guest ;  
  
-   在验证了用户身份的数据库上启用 TRUSTWORTHY 属性。  
  
    `ALTER DATABASE AdventureWorks SET TRUSTWORTHY ON;`  
  

