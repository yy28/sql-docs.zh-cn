---
title: sp_enumeratependingschemachanges (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 74841a258582acce3d9d5a30aa19cd9f000bdb8e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32990802"
---
# <a name="spenumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回所有的挂起架构更改的列表。 此存储的过程可以用于[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)，这使管理员能够跳过挂起的架构更改所选，以便它们不会复制。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] *****发布*****  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@starting_schemaversion=** ] *starting_schemaversion*  
 要包含在结果集中的最低编号的架构更改。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|架构更改应用到项目的名称或**发布级**进行架构更改应用于整个发布。|  
|**schemaversion**|**int**|挂起的架构更改的编号。|  
|**schematype**|**sysname**|表示架构更改类型的文本值。|  
|**schematext**|**nvarchar(max)**|说明架构更改的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。|  
|**schemastatus**|**nvarchar(10)**|指示架构更改是否针对项目挂起，可以是下列值之一：<br /><br /> **active** = 架构更改处于挂起状态<br /><br /> **非活动**= 架构更改处于非活动状态<br /><br /> **跳过**= 不复制架构更改|  
|**schemaguid**|**uniqueidentifier**|标识架构更改。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_enumeratependingschemachanges**合并复制中使用。  
  
 **sp_enumeratependingschemachanges**、 用于[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)、 适用于合并复制可支持性和应仅当其他纠正措施，如重新初始化，无法纠正这种情况。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_enumeratependingschemachanges**。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40;Transact SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
