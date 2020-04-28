---
title: sys. dm_os_performance_counters （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5c7b4d78f73af003e93bc662f10f1f95acda2b6a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265713"
---
# <a name="sysdm_os_performance_counters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为服务器维护的每个性能计数器返回一行。 有关每个性能计数器的信息，请参阅[使用 SQL Server 对象](../../relational-databases/performance-monitor/use-sql-server-objects.md)。  
  
> [!NOTE]  
>  若要从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]调用此，请使用名称**dm_pdw_nodes_os_performance_counters**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|该计数器所属的类别。|  
|**counter_name**|**nchar(128)**|计数器的名称。 若要获取有关计数器的详细信息，这是要从[使用 SQL Server 对象](../../relational-databases/performance-monitor/use-sql-server-objects.md)的计数器列表中选择的主题的名称。 |  
|**instance_name**|**nchar(128)**|计数器特定实例的名称。 通常包含数据库名称。|  
|**cntr_value**|**bigint**|计数器的当前值。<br /><br /> **注意：** 对于每秒计数器，此值为累积值。 速率值必须通过对离散时间间隔的值抽样来进行计算。 任何两个连续抽样值之间的差等于针对所使用时间间隔的速率。|  
|**cntr_type**|**int**|Windows 性能体系结构定义的计数器类型。 有关性能计数器类型的详细信息，请参阅文档中的[WMI 性能计数器类型](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-performance-counter-types)或 Windows Server 文档。|  
|**pdw_node_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="remarks"></a>备注  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安装实例无法显示 Windows 操作系统的性能计数器，请使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询来确定性能计数器是否已被禁用。  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 如果返回值为 0 行，表示性能计数器已被禁用。 然后，您应该查看安装日志，搜索错误 3409，“请为此实例重新安装 sqlctr.ini，并确保实例登录帐户具有正确的注册表权限。”  这说明性能计数器没有启用。 紧邻 3409 错误之前的错误应该指示无法启用性能计数器的根本原因。 有关安装程序日志文件的详细信息，请参阅[查看和读取 SQL Server 安装日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
## <a name="permission"></a>权限

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要权限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层上，需要`VIEW DATABASE STATE`具有数据库中的权限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   
 
## <a name="examples"></a>示例  
 下面的示例返回性能计数器值。  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>另请参阅  
  [&#40;Transact-sql 的与操作系统相关的动态管理视图 SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


