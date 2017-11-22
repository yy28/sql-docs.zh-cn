---
title: MSSQLSERVER_5235 | Microsoft Docs
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5235 (Database Engine error)
ms.assetid: 1aa7e6a5-7ccb-43c8-a1fd-d50e92e0a798
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b786414c1fdd53d21148ff7b682f0b030362afe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver5235"></a>MSSQLSERVER_5235
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5235|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_ERRORLOG_SUMMARY_PREMATURE_TERMINATION|  
|消息正文|[EMERGENCY] 由于错误状态 ERROR_STATE，由 USER_NAME 执行的 DBCC DBCC_COMMAND_DETAILS 已异常终止。 占用时间: HOURS 小时 MINUTES 分钟 SECONDS 秒。|  
  
## <a name="explanation"></a>解释  
这是命令运行时出现意外终止的情况下 DBCC 输出到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志的摘要消息。 消息中报告的错误状态定义了意外终止的类型。  
  
下表列出并定义了错误状态。  
  
|错误状态|定义|  
|---------------|--------------|  
|状态 1|该语句由于元数据损坏而终止。 出现此消息时伴随有错误 8930 的一个或多个实例。|  
|状态 2|该语句由于内部检查失败而终止。 出现此消息时伴随有错误 8967 的一个或多个实例。|  
|状态 3|核心存储引擎系统表的基本系统表检查失败。 出现此消息时伴随有错误 [7984](../../relational-databases/errors-events/mssqlserver-7984-database-engine-error.md)、7985、[7986](~/relational-databases/errors-events/mssqlserver-7986-database-engine-error.md)、[7987](~/relational-databases/errors-events/mssqlserver-7987-database-engine-error.md) 或 [7988](~/relational-databases/errors-events/mssqlserver-7988-database-engine-error.md) 的一个或多个实例。|  
|状态 4|DBCC 紧急模式修复失败，因为重新生成事务日志后无法启动数据库。 出现此消息时，同时出现错误 7909。|  
|状态 5|执行命令时出现断言失败或访问冲突。|  
|状态 6|出现意外终止了 DBCC 命令的未知故障。|  
|状态 7|由于副本 (AlwaysOn) 错误出现的异常终止。|  
  
## <a name="user-action"></a>用户操作  
下表提供了适用于指定错误状态的用户操作。  
  
|错误状态|用户操作|  
|---------------|---------------|  
|状态 1|从备份还原。|  
|状态 2|请联系 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客户服务与支持部门 (CSS)。|  
|状态 3|从备份还原。|  
|状态 4|从备份还原。|  
|状态 4|请与 CSS 联系。|  
|状态 6|再次运行该命令。 如果问题仍然存在，请联系 CSS。|  
  
## <a name="see-also"></a>另请参阅  
[DBCC (Transact-SQL)](~/t-sql/database-console-commands/dbcc-transact-sql.md)  
  
