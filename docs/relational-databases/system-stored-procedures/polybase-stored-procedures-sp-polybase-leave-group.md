---
title: sp_polybase_leave_group (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: rothja
ms.author: jroth
ms.openlocfilehash: 0071746f2d65dd0c9c699beeacf404bf3dd7bb65
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941928"
---
# <a name="sppolybaseleavegroup-transact-sql"></a>sp_polybase_leave_group (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  从横向扩展计算 PolyBase 组中删除 SQL Server 实例。 
 
 SQL Server 实例都必须具有[PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)安装功能。  PolyBase 支持非 SQL Server 数据源，例如 Hadoop 和 Azure blob 存储的集成。 另请参阅[sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>权限  
 要求具有 CONTROL SERVER 权限。  
  
## <a name="remarks"></a>备注  
 仅可以从组中删除计算节点。  
  
 运行后的存储的过程，重启 PolyBase 引擎和 PolyBase 数据移动服务在计算机上。 若要验证的头节点上运行以下 DMV: **sys.dm_exec_compute_nodes**。  
  
## <a name="example"></a>示例  
 该示例从 PolyBase 组中删除当前的计算机。  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>请参阅  
 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
