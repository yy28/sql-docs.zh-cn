---
title: sys.servers (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- servers_TSQL
- sys.servers_TSQL
- servers
- sys.servers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.servers catalog view
ms.assetid: 4e774ed9-4e83-4726-9f1d-8efde8f9feff
caps.latest.revision: 53
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e8c70890bf8571621cd82aaab7e3d2796eb3bb0e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038810"
---
# <a name="sysservers-transact-sql"></a>sys.servers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  包含链接服务器或远程服务器注册，每行和本地服务器具有一个行**server_id** = 0。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|链接服务器的本地 ID。|  
|**名称**|**sysname**|当**server_id** = 0，这是服务器名称。<br /><br /> 当**server_id** > 0，这是链接服务器的本地名称。|  
|**product**|**sysname**|链接服务器的产品名。 “SQL Server”表示这是另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。|  
|**provider**|**sysname**|用于连接到链接服务器的 OLE DB 访问接口名称。|  
|**data_source**|**nvarchar(4000)**|OLE DB 数据源连接属性。|  
|**location**|**nvarchar(4000)**|OLE DB 位置连接属性。 如果没有，则为 NULL。|  
|**provider_string**|**nvarchar(4000)**|OLE DB 访问接口字符串连接属性。<br /><br /> 除非调用方拥有 ALTER ANY LINKED SERVER 权限，否则为 NULL。|  
|**catalog**|**sysname**|OLEDB 目录连接属性。 如果没有，则为 NULL。|  
|**connect_timeout**|**int**|以秒为单位的连接超时，0 表示没有超时。|  
|**query_timeout**|**int**|以秒为单位的查询超时，0 表示没有超时。|  
|**is_linked**|**bit**|0 = 是通过使用添加的旧式服务器**sp_addserver**、 具有不同的 RPC 和分布式事务行为。<br /><br /> 1 = 标准链接服务器。|  
|**is_remote_login_enabled**|**bit**|设置 RPC 选项来启用该服务器的传入远程登录。|  
|**is_rpc_out_enabled**|**bit**|启用（从该服务器的）传出 RPC。|  
|**is_data_access_enabled**|**bit**|为分布式查询启用服务器。|  
|**is_collation_compatible**|**bit**|如果没有可用的排序规则信息，则假定远程数据的排序规则与本地数据兼容。|  
|**uses_remote_collation**|**bit**|如果为 1，则使用远程服务器报告的排序规则；否则，使用下一列指定的排序规则。|  
|**collation_name**|**sysname**|要使用的排序规则的名称，或者，如果只使用本地排序规则，则为 NULL。|  
|**lazy_schema_validation**|**bit**|如果为 1，则在启动查询时不检查架构验证。|  
|**is_system**|**bit**|该服务器只能由内部系统进行访问。|  
|**is_publisher**|**bit**|服务器为复制发布服务器。|  
|**is_subscriber**|**bit**|服务器为复制订阅服务器。|  
|**is_distributor**|**bit**|服务器为复制分发服务器。|  
|**is_nonsql_subscriber**|**bit**|服务器为非 SQL Server 复制订阅服务器。|  
|**is_remote_proc_transaction_promotion_enabled**|**bit**|如果是 1，则调用远程存储过程将启动分布式事务，并用 MS DTC 登记该事务。 有关详细信息，请参阅 [sp_serveroption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)的数据。|  
|**modify_date**|**datetime**|上次更改服务器信息的日期。|  
  
## <a name="permissions"></a>Permissions  
 中的值**provider_string**除非调用方拥有 ALTER ANY LINKED SERVER 权限项始终为 NULL。  
  
 不需要权限以查看本地服务器 (**server_id** = 0)。  
  
 创建链接服务器或远程服务器，当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建默认登录名映射到**公共**服务器角色。 也就是说在默认情况下，所有登录名都可以查看所有链接服务器和远程服务器。 若要将可见性限制为这些服务器，删除默认登录映射通过执行[sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)并指定为 NULL 来*locallogin*参数。  
  
 如果删除了默认登录映射，则只有已作为链接登录名或远程登录名显式添加的用户才能查看其拥有登录名的链接服务器或远程服务器。 删除默认登录映射之后，查看所有的链接服务器和远程服务器需要以下权限：  
  
-   ALTER ANY LINKED SERVER 或 ALTER ANY LOGIN ON SERVER  
  
-   中的成员身份**setupadmin**或**sysadmin**固定服务器角色的成员  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [链接的服务器目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addremotelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
  
