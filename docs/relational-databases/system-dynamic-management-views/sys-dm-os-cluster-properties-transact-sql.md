---
title: sys.dm_os_cluster_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_properties_TSQL
- sys.dm_os_cluster_properties
- dm_os_cluster_properties_TSQL
- dm_os_cluster_properties
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_cluster_properties
- sys.dm_os_cluster_properties
ms.assetid: 6d82e770-fba7-49e0-9a0c-3b34b393e4a7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3fd3c53f5603567e0f6c2b6ee4f1712f742c1137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900231"
---
# <a name="sysdmosclusterproperties-transact-sql"></a>sys.dm_os_cluster_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为本主题中确定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 群集资源属性的当前设置返回一行。 如果此视图是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的独立实例上运行，则不会返回任何数据。  
  
 使用这些属性设置的值将影响故障检测、故障响应时间以及用于监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例的运行状况的日志记录。  
  

|列名|属性|描述|  
|-----------------|--------------|-----------------|  
|VerboseLogging|BIGINT|SQL Server 故障转移群集的日志记录级别。 可以通过启用详细日志记录在错误日志中提供更多详细信息以排除故障。 以下值之一：<br /><br /> 0 - 关闭日志记录（默认值）<br /><br /> 1 - 仅限错误<br /><br /> 2 - 错误和警告<br /><br /> 有关详细信息，请参阅[ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)。|  
|SqlDumperDumpFlags|BIGINT|SQLDumper 转储标志确定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的转储文件的类型。 默认设置为 0。|  
|SqlDumperDumpPath|nvarchar(260)|SQLDumper 实用工具生成转储文件的位置。|  
|SqlDumperDumpTimeOut|BIGINT|超时值（毫秒），一旦 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 失败，SQLDumper 实用工具即在该超时值后生成转储。 默认值为 0。|  
|FailureConditionLevel|BIGINT|设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集应在哪些状况下失败或重新启动。 默认值为 3。 有关详细说明或要更改的属性设置，请参阅[Configure FailureConditionLevel Property Settings](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)。|  
|HealthCheckTimeout|BIGINT|超时值，即 SQL Server 数据库引擎资源 DLL 在认定 SQL Server 实例不响应之前应等待服务器运行状况信息的时间。 该超时值用毫秒表示。 默认值为 60000。 有关详细信息或要更改此属性设置，请参阅[Configure HealthCheckTimeout Property Settings](../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)。|  
  
## <a name="permissions"></a>权限  
 需要对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例具有 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
 下面的示例使用 sys.dm_os_cluster_properties 返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集资源的属性设置。  
  
```  
SELECT VerboseLogging, SqlDumperDumpFlags, SqlDumperDumpPath, SqlDumperDumpTimeOut, FailureConditionLevel, HealthCheckTimeout  
FROM sys.dm_os_cluster_properties;  
```  
  
 下面是一个结果集示例。  
  
|VerboseLogging|SqlDumperDumpFlags|SqlDumperDumpPath|SqlDumperDumpTimeOut|FailureConditionLevel|HealthCheckTimeout|  
|--------------------|------------------------|-----------------------|--------------------------|---------------------------|------------------------|  
|0|0|NULL|0|3|60000|  
  
  
