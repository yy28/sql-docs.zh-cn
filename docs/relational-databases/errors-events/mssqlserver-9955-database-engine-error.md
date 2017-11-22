---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5ac734473c592a347c8c954d7815b43869d3b9c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9955"></a>MSSQLSERVER_9955
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9955|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|FTXT2_MSSEARCHACCESSDENY|  
|消息正文|SQL Server 无法创建命名管道 '%ls' 以与全文筛选器后台程序通信(Windows 错误: %d)。 筛选器后台主机进程已有一个命名管道，系统资源不足，或者对筛选器后台程序帐户组的安全标识号(SID)查找失败。 若要纠正此错误，请终止任何正在运行的全文筛选器后台进程，并在必要时重新配置全文后台程序启动程序服务帐户。|  
  
## <a name="explanation"></a>解释  
当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法创建用来与全文筛选器后台程序通信的命名管道时，会出现此消息。 筛选器后台主机进程已有一个命名管道，系统资源不足，或者对筛选器后台程序帐户组的安全标识号(SID)查找失败。  
  
## <a name="user-action"></a>用户操作  
若要纠正此错误，请终止任何正在运行的全文筛选器后台进程，并在必要时使用 SQL Server 配置管理器重新配置全文后台程序主机帐户。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 配置管理器](~/relational-databases/sql-server-configuration-manager.md)  
[设置用于全文筛选器后台程序启动器的服务帐户](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[全文搜索](~/relational-databases/search/full-text-search.md)  
  
