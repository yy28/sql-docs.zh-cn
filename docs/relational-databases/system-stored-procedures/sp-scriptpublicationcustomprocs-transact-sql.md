---
title: sp_scriptpublicationcustomprocs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3c6a24a03e1ac8b4fff3fe4af878f051cf2e35a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815447"
---
# <a name="spscriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在启用了自动生成自定义过程架构选项的发布中，为所有表项目编写自定义 INSERT、UPDATE 和 DELETE 过程的脚本。 **sp_scriptpublicationcustomprocs**设置为其手动应用快照的订阅特别有用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication**=] **'***publication_name*****  
 发布的名称。 *publication_name*是**sysname** ，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 返回一个结果集包含单个**nvarchar(4000)** 列。 该结果集构成创建自定义存储过程所需的完整 CREATE PROCEDURE 语句。  
  
## <a name="remarks"></a>备注  
 如果未启用自动生成自定义过程 (0x2) 架构选项，则不会为项目编写自定义过程的脚本。  
  
 通过使用下列过程**sp_scriptpublicationcustomprocs**创建订阅服务器的过程，并且不应直接执行：  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>Permissions  
 执行权限授予**公共**; 若要限制对成员的访问此存储过程内执行过程安全性检查**sysadmin**固定的服务器角色和**db_所有者**当前数据库中的固定的数据库角色。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
