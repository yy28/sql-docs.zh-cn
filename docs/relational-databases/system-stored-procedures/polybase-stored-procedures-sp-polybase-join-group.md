---
title: sp_polybase_join_group |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cffdf311abbac196b49a5174364d8f313275ad40
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038960"
---
# <a name="sppolybasejoingroup-transact-sql"></a>sp_polybase_join_group (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  将 SQL Server 实例作为计算节点添加到 PolyBase 组中的横向扩展计算。  
  
 SQL Server 实例都必须具有[PolyBase](../../relational-databases/polybase/polybase-guide.md)安装功能。  PolyBase 支持非 SQL Server 数据源，例如 Hadoop 和 Azure blob 存储的集成。 另请参阅[sp_polybase_leave_group &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>参数  
 *@head_node_address* = N'*head_node_address*'  
 托管 SQL Server 的 PolyBase 横向扩展组的头节点的计算机的名称。 *@head_node_address* 是 nvarchar(255)。  
  
 *@dms_control_channel_port* = dms_control_channel_port  
 PolyBase 数据移动服务的头节点的控制通道正在其中运行的端口。 *@dms_control_channel_port* 是无符号的 __int16。 默认值是**16450**。  
  
 *@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 PolyBase 横向扩展组中的头节点 SQL Server 实例的名称。 *@head_node_sql_server_instance_name* 是 nvarchar(16)。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 权限。  
  
## <a name="remarks"></a>Remarks  
 运行存储的过程之后, 关闭 PolyBase 引擎和重启 PolyBase 数据移动服务在计算机上。 若要验证的头节点上运行以下 DMV: **sys.dm_exec_compute_nodes**。  
  
## <a name="example"></a>示例  
 该示例为计算节点到 PolyBase 组联接在当前计算机。  在头节点的名称是**HST01** ，在头节点上的 SQL Server 实例名为**MSSQLSERVER**。  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>请参阅  
 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
