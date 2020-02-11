---
title: sp_removedistpublisherdbreplication （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 49c06ac45a91014199caa75c5893971f6f3de715
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771034"
---
# <a name="sp_removedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  删除属于分发服务器上的特定发布的发布元数据。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'`发布服务器的名称。 *发布服务器*的**sysname**，无默认值。  
  
`[ @publisher_db = ] 'publisher_db'`发布数据库的名称。 *publisher_db* **sysname** ，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_removedistpublisherdbreplication**由事务复制和快照复制使用。  
  
 当必须在不删除分发数据库的情况下重新创建已发布的数据库时，将使用**sp_removedistpublisherdbreplication** 。 将删除下列元数据：  
  
-   所有的发布元数据。  
  
-   属于该发布的所有项目的元数据。  
  
-   发布的全部订阅的元数据。  
  
-   属于发布的所有复制代理作业的元数据。  
  
## <a name="permissions"></a>权限  
 只有分发服务器上**sysadmin**固定服务器角色的成员或分发数据库中**db_owner**固定数据库角色的成员才能执行**sp_removedistpublisherdbreplication**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
