---
title: sp_helpreplicationdboption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c67c6c6f6f74d3cedf2aa8acc4232886b6d52a9f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038749"
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示是否为发布服务器上的数据库启用复制。 此存储过程在发布服务器的任何数据库中执行。 *不支持 Oracle 发布服务器。*  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@dbname=**] **'***dbname***'**  
 数据库的名称。 *dbname*是**sysname**，默认值为**%**。 如果**%**，则结果集包含发布服务器上的所有数据库，否则指定的数据库上的唯一信息返回。 如下所述，将不会返回用户对其不具有适当权限的任何数据库的信息。  
  
 [  **@type=**] **'***类型*****  
 结果集要包含仅在其上的数据库限制为指定的复制选项*类型*值已启用。 *类型*是**sysname**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**发布**|允许事务复制。|  
|**合并发布**|允许合并复制。|  
|**复制允许**（默认值）|允许事务复制或合并复制。|  
  
 [  **@reserved=** ]*保留*  
 指定是否返回有关现有发布和订阅的信息。 *保留*是**位**，默认值为 0。 如果**1**，则结果集包含有关指定的数据库具有任何现有发布或订阅的信息。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|数据库的名称。|  
|**id**|**int**|数据库标识符。|  
|**transpublish**|**bit**|如果该数据库启用快照或事务发布;其中的值**1**表示启用快照或事务发布。|  
|**mergepublish**|**bit**|如果已启用数据库进行合并发布;其中的值**1**启用合并发布的方式。|  
|**dbowner**|**bit**|如果用户是属于**db_owner**固定数据库角色; 当值为**1**指出该用户是此角色的成员。|  
|**dbreadonly**|**bit**|是如果将数据库标记为只读的;其中的值**1**意味着数据库是只读的。|  
|**haspublications**|**bit**|是该数据库是否有任何现有发布;其中的值**1**意味着现有发布。|  
|**haspullsubscriptions**|**bit**|是该数据库是否有任何现有的请求订阅;其中的值**1**意味着存在现有请求订阅。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_helpreplicationdboption**快照、 事务和合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 成员**sysadmin**固定的服务器角色可以执行**sp_helpreplicationdboption**的任何数据库。 成员**db_owner**固定的数据库角色可以执行**sp_helpreplicationdboption**该数据库。  
  
## <a name="see-also"></a>请参阅  
 [sp_replicationdboption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
