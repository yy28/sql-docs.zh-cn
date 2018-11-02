---
title: sys.dm_external_script_execution_stats |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_execution_stats
- sys.dm_external_script_execution_stats_TSQL
- dm_external_script_execution_stats
- dm_external_script_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_execution_stats dynamic management view
ms.assetid: 2e99f026-ceb2-42a2-a549-c71d31ed0cf4
author: HeidiSteen
ms.author: heidist
manager: cgronlund
ms.openlocfilehash: 8bdbaf1fdb0fb0c27127611ace0fac00d861838f
ms.sourcegitcommit: c2322c1a1dca33b47601eb06c4b2331b603829f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50743132"
---
# <a name="sysdmexternalscriptexecutionstats"></a>sys.dm_external_script_execution_stats
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

为每种类型的外部脚本请求返回一行。 外部脚本请求由受支持的外部脚本语言分组。 为每个已注册的外部脚本函数生成一行。 除非是由父进程（如 `rxExec`）发送，否则不会记录任意外部脚本函数。
  
> [!NOTE]  
> 仅当已安装并启用支持外部脚本执行的功能，此动态管理视图 (DMV) 是可用。 有关详细信息，请参阅[SQL Server 2016 中的 R Services](../../advanced-analytics/r/sql-server-r-services.md)并[中的机器学习服务 （R、 Python） SQL Server 2017](../../advanced-analytics/what-is-sql-server-machine-learning.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|language|**nvarchar**|已注册的外部脚本语言的名称。 每个外部脚本必须在脚本请求中指定语言以启动关联的启动器。 |  
|counter_name|**nvarchar**|已注册的外部脚本函数的名称。 不可为 null。|  
|counter_value|**integer**|已在服务器上调用已注册外部脚本函数的实例的总数。 此值是累计的（从在实例上安装该功能的时间开始），且不能重置。|  

  
## <a name="permissions"></a>Permissions  
 需要针对服务器的 VIEW SERVER STATE 权限。  
  
> [!NOTE]  
>  运行外部脚本的用户必须具有额外权限 EXECUTE ANY EXTERNAL SCRIPT，但是，此 DMV 可由没有此权限的管理员使用。 
  
## <a name="remarks"></a>备注  
  此 DMV 为内部遥测提供，以监视 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中提供的新外部脚本执行功能的总体使用情况。 启动 LaunchPad 时会启动遥测服务，每次调用已注册的外部脚本函数时会递增基于磁盘的计数器。

通常情况下，只要生成性能计数器的进程处于活动状态，它们便有效。 因此，对 DMV 的查询不能显示已停止运行的服务的详细数据。 例如，如果启动程序执行外部脚本，并且尚未完成其得非常快，常规 DMV 可能不会显示任何数据。

因此，即使实例已关闭，此 DMV 所跟踪的计数器仍会保持运行，并且通过使用写入到磁盘保留 sys.dm_external_script_requests 的状态。

   
  
### <a name="counter-values"></a>计数器值
SQL Server 2016 中支持的唯一的外部语言是 R 和外部脚本请求由处理[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。 在 SQL Server 2017 中，R 和 Python 均受支持的外部语言和外部脚本请求由处理[!INCLUDE[rsql_productname_md](../../includes/rsql-productnamenew-md.md)]。

对于 R，此 DMV 会跟踪实例上的 R 调用所做的次数。 例如，如果调用且并行运行了 `rxLinMod` ，该计数器会增大 1。
 
对于 R 语言， *counter_name* 字段中显示的计数器值表示已注册的 ScaleR 函数的名称。 *counter_value* 字段中的值表示特定 ScaleR 函数实例的累计数。 

对于 Python，此 DMV 会跟踪实例上的 Python 进行的调用数。

在实例上安装并启用该功能时，计数开始；计数会一直累积，直到删除维护状态的文件或管理员将该文件覆盖。 因此，通常不可能重置 *counter_value*中的值。 如要希望根据会话、日历时间和其他间隔来监视使用情况，我们建议将计数捕获到表中。

### <a name="registration-of-external-script-functions-in-r"></a>在 R 中的外部脚本函数的注册

R 支持任意脚本，R 社区提供了许多几千个包，每个都有其自己的函数和方法。 但是，此 DMV 仅监视随 SQL Server R Services 一起安装的 ScaleR 函数。

安装该功能时将执行这些函数的注册，而且不能添加或删除已注册的函数。

## <a name="examples"></a>示例  
  
### <a name="viewing-the-number-of-r-scripts-run-on-the-server"></a>查看服务器上运行的 R 脚本的数量  
 下面的示例显示 R 语言的外部脚本执行的累计数。  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'R';
```  

### <a name="viewing-the-number-of-python-scripts-run-on-the-server"></a>在服务器上运行查看数量的 Python 脚本  
 以下示例显示 Python 语言的外部脚本执行的累计数量。  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'Python';
```  

  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与执行相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md) 
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

