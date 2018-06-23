---
title: default trace enabled 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bb4067c2bbb5f922dd8e70b50acaaccb1a1955af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127148"
---
# <a name="default-trace-enabled-server-configuration-option"></a>default trace enabled 服务器配置选项
  使用 **default trace enabled** 选项可启用或禁用默认跟踪日志文件。 默认跟踪功能提供了丰富持久的活动日志，并主要根据配置选项进行更改。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件。  
  
## <a name="purpose"></a>用途  
 默认跟踪可确保数据库管理员在问题首次出现时即具有诊断该问题所需的日志数据，从而为数据库管理员提供了故障排除帮助。  
  
## <a name="viewing"></a>查看  
 默认跟踪日志可以通过 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 打开和检查，或者通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 使用 `fn_trace_gettable` 系统函数来查询。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 可以像打开正常跟踪输出文件一样打开默认跟踪日志文件。 默认情况下，默认跟踪日志以滚动更新跟踪文件的形式存储在 `\MSSQL\LOG` 目录中。 默认跟踪日志文件的基本文件名是 `log.trc`。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的典型安装中，默认跟踪启用并因而成为 TraceID 1。 如果在安装和创建其他跟踪后启用，该 TraceID 可以变成更大的数字。  
  
 有关使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件探查器查看此跟踪文件的详细信息，请参阅[打开跟踪文件 (SQL Server Profiler)](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)。  
  
### <a name="example"></a>例如：  
 以下语句将打开默认位置中的默认跟踪日志：  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>配置  
 如果将 **default trace enabled** 选项设置为 1，可启用“默认跟踪” 。 此选项的默认设置为 1 (ON)。 值为 0 时将关闭跟踪。  
  
 **default trace enabled** 选项是一个高级选项。 如果使用 **sp_configure** 系统存储过程来更改该设置，则仅当 **show advanced options** 设置为 1 时才能更改 **default trace enabled** 选项。 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>请参阅  
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
