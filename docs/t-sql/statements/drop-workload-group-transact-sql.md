---
title: "DROP WORKLOAD GROUP (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs: TSQL
helpviewer_keywords: DROP WORKLOAD GROUP statement
ms.assetid: 1cd68450-5b58-4106-a2bc-54197ced8616
caps.latest.revision: "23"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5211e91f9bd1e6dc8dd49676c024b3356163538
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除现有的用户定义资源调控器工作负荷组。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP WORKLOAD GROUP group_name  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *group_name*  
 现有的用户定义工作负荷组的名称。  
  
## <a name="remarks"></a>注释  
 不允许对资源调控器内部组或默认组使用 DROP WORKLOAD GROUP 语句。  
  
 建议您在熟悉资源调控器状态之后再执行 DDL 语句。 有关详细信息，请参阅[资源调控器](../../relational-databases/resource-governor/resource-governor.md)。  
  
 如果工作负荷组包含活动会话，则调用 ALTER RESOURCE GOVERNOR RECONFIGURE 语句以应用更改时，删除工作负荷组或将其移至其他资源池的操作将失败。 若要避免此问题，可以执行以下操作之一：  
  
-   等待受影响组的所有会话均断开连接，然后重新运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。  
  
-   使用 KILL 命令显式停止受影响的组中的会话，然后重新运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。  
  
-   重新启动服务器。 完成重新启动过程后，将不会创建已删除的组，并且已移动的组将使用新分配的资源池。  
  
-   在已发出 DROP WORKLOAD GROUP 语句但决定不打算显式停止会话以应用更改的情况下，您可以使用在发出 DROP 语句之前组的名称来重新创建组，然后将该组移动到原始资源池。 若要应用更改，请运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。  
  
## <a name="permissions"></a>权限  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例删除名为的工作负荷组`adhoc`。  
  
```  
DROP WORKLOAD GROUP adhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
