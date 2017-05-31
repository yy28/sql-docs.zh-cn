---
title: "筛选跟踪 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6315705010a41afb985682e63338cc95237b5e78
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="filter-a-trace"></a>筛选跟踪
  筛选器将限制跟踪内收集的事件。 如果没有设置筛选器，则跟踪输出中将返回选定事件类的所有事件。 例如，如果将跟踪中的 Windows 用户名限定为特定用户，将仅输出与那些用户相关的数据。  
  
 并不一定要为跟踪设置筛选器。 但是，筛选器会将跟踪过程中的开销降到最低。 筛选器将返回有针对性的数据，这样会使性能分析和审核变得更容易。  
  
 若要筛选跟踪中捕获的事件数据，请选择跟踪事件准则（仅返回跟踪中的相关数据）。 例如，可以包括或排除监视跟踪中的特定应用程序的活动。  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 创建跟踪时，默认情况下，将筛选出自己的活动。  
  
 又如，如果监视查询以确定执行时间最长的批处理，请将跟踪事件准则设置为仅监视那些执行时间超过 30 秒的批处理（CPU 最小值为 30,000 毫秒）。  
  
## <a name="filter-creation-guidelines"></a>筛选器创建指南  
 通常，按照下列步骤筛选跟踪。  
  
1.  在跟踪中标识要包括的事件。  
  
2.  标识包含所需信息的数据和数据列。  
  
3.  标识所需数据的子集并基于该数据子集定义筛选器。  
  
 例如，您可能只对超过一定时间长度的事件感兴趣。 您可以创建包括事件（其中 **Duration** 数据列超过 300 毫秒）的跟踪。 跟踪将不包括在 300 毫秒内完成的事件。  
  
 您可以使用 SQL Server Profiler 或 Transact-SQL 存储过程创建筛选器。  
  
 **在跟踪模板中筛选事件**  
  
 [在跟踪中筛选事件 (SQL Server Profiler)](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
 [设置跟踪筛选器 (Transact-SQL)](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
 **修改筛选器**  
  
 [修改筛选器 (SQL Server Profiler)](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 筛选器可用性取决于数据列。 某些数据列无法筛选。 可筛选的数据列只能使用部分关系运算符进行筛选，如下表所示。  
  
|关系运算符|运算符|说明|  
|-------------------------|---------------------|-----------------|  
|Like|Like|指定跟踪事件数据必须类似于输入文本。 允许使用多个值。|  
|不类似于|不类似于|指定跟踪事件数据不能与输入文本类似。 允许使用多个值。|  
|等于|=|指定跟踪事件数据必须等于输入的值。 允许使用多个值。|  
|不等于|<>|指定跟踪事件数据不能等于输入的值。 允许使用多个值。|  
|大于|>|指定跟踪事件数据必须大于输入的值。|  
|大于或等于|>=|指定跟踪事件数据必须大于或等于输入的值。|  
|小于|<|指定跟踪事件数据必须小于输入的值。|  
|小于或等于|<=|指定跟踪事件数据必须小于或等于输入的值。|  
  
 下表列出了可筛选数据列和可用关系运算符。  
  
|数据列|关系运算符|  
|------------------|--------------------------|  
|**ApplicationName**|LIKE、NOT LIKE|  
|**BigintData1**|=, <>, >=, <=|  
|**BigintData2**|=, <>, >=, <=|  
|**BinaryData**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 筛选此数据列中的事件。 有关详细信息，请参阅 [使用 SQL Server Profiler 筛选跟踪](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**ClientProcessID**|=, <>, >=, <=|  
|**ColumnPermissions**|=, <>, >=, <=|  
|**CPU**|=, <>, >=, <=|  
|**DatabaseID**|=, <>, >=, <=|  
|**DatabaseName**|LIKE、NOT LIKE|  
|**DBUserName**|LIKE、NOT LIKE|  
|**Duration**|=, <>, >=, \<=|  
|**EndTime**|>=, <=|  
|**错误**|=, <>, >=, <=|  
|**EventSubClass**|=, <>, >=, <=|  
|**FileName**|LIKE、NOT LIKE|  
|**GUID**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 筛选此数据列中的事件。 有关详细信息，请参阅 [使用 SQL Server Profiler 筛选跟踪](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**Handle**|=, <>, >=, <=|  
|**HostName**|LIKE、NOT LIKE|  
|**IndexID**|=, <>, >=, <=|  
|**IntegerData**|=, <>, >=, <=|  
|**IntegerData2**|=, <>, >=, <=|  
|**IsSystem**|=, <>, >=, <=|  
|**LineNumber**|=, <>, >=, <=|  
|**LinkedServerName**|LIKE、NOT LIKE|  
|**LoginName**|LIKE、NOT LIKE|  
|**LoginSid**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 筛选此数据列中的事件。 有关详细信息，请参阅 [使用 SQL Server Profiler 筛选跟踪](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**MethodName**|LIKE、NOT LIKE|  
|**模式**|=, <>, >=, <=|  
|**NestLevel**|=, <>, >=, <=|  
|**NTDomainName**|LIKE、NOT LIKE|  
|**NTUserName**|LIKE、NOT LIKE|  
|**Exchange Spill**|=, <>, >=, <=|  
|**ObjectID2**|=, <>, >=, <=|  
|**ObjectName**|LIKE、NOT LIKE|  
|**ObjectType**|=, <>, >=, <=|  
|**Offset**|=, <>, >=, <=|  
|**OwnerID**|=, <>, >=, <=|  
|**OwnerName**|LIKE、NOT LIKE|  
|**ParentName**|LIKE、NOT LIKE|  
|**权限**|=, <>, >=, <=|  
|**ProviderName**|LIKE、NOT LIKE|  
|**Reads**|=, <>, >=, <=|  
|**RequestID**|=, <>, >=, <=|  
|**RoleName**|LIKE、NOT LIKE|  
|**RowCounts**|=, <>, >=, <=|  
|**SessionLoginName**|LIKE、NOT LIKE|  
|**Severity**|=, <>, >=, <=|  
|**SourceDatabaseID**|=, <>, >=, <=|  
|**SPID**|=, <>, >=, \<=|  
|**SqlHandle**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 筛选此数据列中的事件。 有关详细信息，请参阅 [使用 SQL Server Profiler 筛选跟踪](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**StartTime**|>=, <=|  
|**State**|=, <>, >=, <=|  
|**成功**|=, <>, >=, <=|  
|**TargetLoginName**|LIKE、NOT LIKE|  
|**TargetLoginSid**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 筛选此数据列中的事件。 有关详细信息，请参阅 [使用 SQL Server Profiler 筛选跟踪](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**TargetUserName**|LIKE、NOT LIKE|  
|**TextData** *|LIKE、NOT LIKE|  
|**TransactionID**|=, <>, >=, <=|  
|**类型**|=, <>, >=, <=|  
|**Writes**|=, <>, >=, <=|  
|**XactSequence**|=, <>, >=, <=|  
  
 \* 如果从 **osql** 实用工具或 **sqlcmd** 实用工具跟踪事件，则始终将 **%** 追加到 **TextData** 数据列上的筛选器。  
  
 SQL 跟踪作为一种安全预防措施，会自动从跟踪中省略任何影响密码的、与安全相关的存储过程。 此安全机制不可配置，并且始终有效。 此机制阻止有权跟踪 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的所有活动的用户捕获密码。  
  
 下列与安全相关的存储过程会受到监视，而不会将输出写入 **TextData** 数据列：  
  
 [sp_addapprole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)  
  
 [sp_adddistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)  
  
 [sp_adddistributiondb (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)  
  
 [sp_adddistributor (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)  
  
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
 [sp_addlinkedsrvlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)  
  
 [sp_addmergepullsubscription_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 [sp_addpullsubscription_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
 [sp_addremotelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
 [sp_addsubscriber (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)  
  
 [sp_approlepassword (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-approlepassword-transact-sql.md)  
  
 [sp_changedistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)  
  
 [sp_changesubscriber (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)  
  
 [sp_dsninfo (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)  
  
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
 [sp_link_publication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)  
  
 [sp_password (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)  
  
 [sp_setapprole (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)  
  
  
