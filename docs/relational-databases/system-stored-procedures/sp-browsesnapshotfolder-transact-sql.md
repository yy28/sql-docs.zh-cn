---
title: sp_browsesnapshotfolder (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fff4d6ca3c05e75dfbbfb756abcec6540cd33949
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spbrowsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回为发布生成的最新快照的完整路径。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 包含项目的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@subscriber=**] *****订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_db=**] *****subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|快照目录的完整路径。|  
  
## <a name="remarks"></a>注释  
 **sp_browsesnapshotfolder**快照复制和事务复制中使用。  
  
 如果*订阅服务器*和*subscriber_db*字段留空，则存储的过程返回的最新的快照它能找到发布的快照文件夹。 如果*订阅服务器*和*subscriber_db*指定字段，该存储的过程返回指定的订阅的快照文件夹。 如果没有为发布生成快照，则返回空结果集。  
  
 如果将发布设置为同时在发布服务器的工作目录和发布服务器的快照文件夹中生成快照文件，则结果集将包含两行。 第一行包含发布快照文件夹，第二行包含发布服务器工作目录。 **sp_browsesnapshotfolder**可用于确定其中生成快照文件的目录。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_browsesnapshotfolder**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
