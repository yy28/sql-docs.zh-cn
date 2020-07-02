---
title: sp_browsemergesnapshotfolder （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsemergesnapshotfolder
- sp_browsemergesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsemergesnapshotfolder
ms.assetid: e248642f-5fea-4ed7-be1a-36ff75abcfde
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5c930347c18dc257b5a6c51d2b013d2429b269fe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715991"
---
# <a name="sp_browsemergesnapshotfolder-transact-sql"></a>sp_browsemergesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  返回为合并发布生成的最新快照的完整路径。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_browsemergesnapshotfolder [@publication= ] 'publication'  
```  
  
## <a name="arguments"></a>自变量  
`[ @publication = ] 'publication'`发布的名称。 *发布*为**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar （2000）**|快照目录的完整路径。|  
  
## <a name="remarks"></a>备注  
 **sp_browsemergesnapshotfolder**用于合并复制。  
  
 如果发布被设置为在发布服务器工作目录和发布服务器快照文件夹中都生成快照文件，则结果集包含两行：第一行包含发布快照文件夹，第二行包含发布服务器工作目录。  
  
 **sp_browsemergesnapshotfolder**可用于确定生成合并快照文件的目录。 然后可以将该文件夹/路径及其内容复制到可移动介质，并使用快照从备用快照位置同步订阅。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_browsemergesnapshotfolder**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
