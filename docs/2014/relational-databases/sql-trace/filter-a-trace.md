---
title: 筛选跟踪 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 381007cb26f74cdf945900436d8a9fcea5a4ef39
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714714"
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
  
 [设置跟踪筛选器 (Transact-SQL)](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
 **修改筛选器**  
  
 [修改筛选器 (SQL Server Profiler)](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 筛选器可用性取决于数据列。 某些数据列无法筛选。 可筛选的数据列只能使用部分关系运算符进行筛选，如下表所示。  
  
|关系运算符|运算符|Description|  
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
|**状态**|=, <>, >=, <=|  
|**成功**|=, <>, >=, <=|  
|**TargetLoginName**|LIKE、NOT LIKE|  
|**TargetLoginSid**|使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 筛选此数据列中的事件。 有关详细信息，请参阅 [使用 SQL Server Profiler 筛选跟踪](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)。|  
|**TargetUserName**|LIKE、NOT LIKE|  
|**TextData** <sup>1</sup>|LIKE、NOT LIKE|  
|**TransactionID**|=, <>, >=, <=|  
|**类型**|=, <>, >=, <=|  
|**Writes**|=, <>, >=, <=|  
|**XactSequence**|=, <>, >=, <=|  
  
 <sup>1</sup>如果跟踪中的事件**osql**实用程序或**sqlcmd**实用程序，始终追加**%** 上的筛选器到**TextData**数据列。  
  
 SQL 跟踪作为一种安全预防措施，会自动从跟踪中省略任何影响密码的、与安全相关的存储过程。 此安全机制不可配置，并且始终有效。 此机制阻止有权跟踪 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的所有活动的用户捕获密码。  
  
 下列与安全相关的存储过程会受到监视，而不会将输出写入 **TextData** 数据列：  
  
 [sp_addapprole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addapprole-transact-sql)  
  
 [sp_adddistpublisher (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)  
  
 [sp_adddistributiondb (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)  
  
 [sp_adddistributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)  
  
 [sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
 [sp_addlinkedsrvlogin (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql)  
  
 [sp_addlogin (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)  
  
 [sp_addmergepullsubscription_agent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)  
  
 [sp_addpullsubscription_agent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)  
  
 [sp_addremotelogin (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql)  
  
 [sp_addsubscriber (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql)  
  
 [sp_approlepassword (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-approlepassword-transact-sql)  
  
 [sp_changedistpublisher (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)  
  
 [sp_changesubscriber (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql)  
  
 [sp_dsninfo (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dsninfo-transact-sql)  
  
 [sp_helpsubscription_properties (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)  
  
 [sp_link_publication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)  
  
 [sp_password (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)  
  
 [sp_setapprole (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql)  
  
  
