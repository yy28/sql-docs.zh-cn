---
title: sp_polybase_join_group |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: rothja
ms.author: jroth
ms.openlocfilehash: ba22ffe282e6b4248ed58bed850bc6ac08255df5
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278112"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  将 SQL Server 实例作为计算节点添加到 PolyBase 组，以便进行向外扩展计算。  
  
 SQL Server 实例必须安装[PolyBase](../../relational-databases/polybase/polybase-guide.md)功能。  PolyBase 启用了非 SQL Server 数据源，如 Hadoop 和 Azure blob 存储。 另请[参阅&#40;sp_polybase_leave_group transact-sql&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>参数  
 *\@head_node_address* = N '*head_node_address*'  
 承载 PolyBase 横向扩展组的 SQL Server 头节点的计算机名称。 *\@head_node_address*为 nvarchar （255）。  
  
 *\@dms_control_channel_port* = dms_control_channel_port  
 头节点 PolyBase 数据移动服务的控制通道正在其上运行的端口。 *@no__t 1dms_control_channel_port*是一个无符号 __int16。 默认值为**16450**。  
  
 *\@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 在 PolyBase 横向扩展组中 SQL Server 实例的头节点的名称。 *\@head_node_sql_server_instance_name*为 nvarchar （16）。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>权限  
 需要 CONTROL SERVER 权限。  
  
## <a name="remarks"></a>备注  
 运行存储过程后，关闭 PolyBase 引擎，然后在计算机上重新启动 PolyBase 数据移动服务。 验证在头节点上运行以下 DMV： **_exec_compute_nodes**。  
  
## <a name="example"></a>示例  
 该示例将当前计算机作为计算节点加入 PolyBase 组。  头节点的名称为**HST01** ，头节点上 SQL Server 实例的名称为**MSSQLSERVER**。  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>请参阅  
 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
