---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f3618984aaf0ee8b64ff73ed30c0fe88e5206c2f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013859"
---
# <a name="mssqlserver9955"></a>MSSQLSERVER_9955
    
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
  
## <a name="see-also"></a>请参阅  
 [SQL Server 配置管理器](../sql-server-configuration-manager.md)   
 [设置用于全文筛选器后台程序启动器的服务帐户](../search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [全文搜索](../search/full-text-search.md)  
  
  