---
title: "sys.sysservers (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0b6315f4c0ca23e76381c268a65ba40534314c10
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例可作为 OLE DB 数据源访问的每个服务器都包含一行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**srvid**|**int**|远程服务器的 ID（只限本地使用）。|  
|**srvstatus**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|服务器的名称。|  
|**srvproduct**|**sysname**|远程服务器的产品名称。|  
|**providername**|**nvarchar （128)**|用于访问此服务器的 OLE DB 访问接口名称。|  
|**数据源**|**nvarchar(4000)**|OLE DB 数据源值。|  
|**位置**|**nvarchar(4000)**|OLE DB 位置值。|  
|**providerstring**|**nvarchar(4000)**|OLE DB 访问接口字符串值。|  
|**schemadate**|**datetime**|此行上次更新的日期。|  
|**topologyx**|**int**|未使用。|  
|**topologyy**|**int**|未使用。|  
|**目录**|**sysname**|与 OLE DB 访问接口连接时所用的目录。|  
|**srvcollation**|**sysname**|服务器的排序规则。|  
|**connecttimeout**|**int**|服务器连接的超时设置。|  
|**querytimeout**|**int**|对服务器进行查询的超时设置。|  
|**srvnetname**|**char （30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = 服务器为远程服务器。<br /><br /> 0 = 服务器为链接服务器。|  
|**rpc**|**bit**|1 =  **sp_serveroption@rpc** 设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@rpc** 设置为**false**或**关闭**。|  
|**发布**|**bit**|1 =  **sp_serveroption@pub** 设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@pub** 设置为**false**或**关闭**。|  
|**sub**|**bit**|1 =  **sp_serveroption@sub** 设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@sub** 设置为**false**或**关闭**。|  
|**dist**|**bit**|1 =  **sp_serveroption@dist** 设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@dist** 设置为**false**或**关闭**。|  
|**dpub**|**bit**|1 =  **sp_serveroption@dpub** 设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@dpub** 设置为**false**或**关闭**。|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc出**设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@rpc出**设置为**false**或**关闭**。|  
|**dataaccess**|**bit**|1 =  **sp_serveroption@data访问**设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@data访问**设置为**false**或**关闭**。|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation兼容**设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@collation兼容**设置为**false**或**关闭**。|  
|**系统**|**bit**|1 =  **sp_serveroption@system** 设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@system** 设置为**false**或**关闭**。|  
|**useremotecollation**|**bit**|1 =  **sp_serveroption@remote排序规则**设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@remote排序规则**设置为**false**或**关闭**。|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy架构验证**设置为**true**或**上**。<br /><br /> 0 =  **sp_serveroption@lazy架构验证**设置为**false**或**关闭**。|  
|**排序规则**|**sysname**|如所设置的服务器排序规则**sp_serveroption@collation名称**。|  
|**nonsqlsub**|bit|0 = 服务器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例<br /><br /> 1 = 服务器不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
