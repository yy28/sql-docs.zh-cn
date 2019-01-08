---
title: sp_publisherproperty (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 49be961d1bc34bcc06b046e95b73d0b5c8ed33ac
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204396"
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示或更改发布服务器属性的非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 此存储过程在分发服务器上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>参数  
 [**@publisher** =] **'***发布服务器***’**  
 异类发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [**@propertyname** =] **'***propertyname***’**  
 所设置的属性的名称。 *propertyname*是**sysname**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**xactsetbatching**|是否将发布服务器上的事务分组成在事务上一致的集合（称为 Xactset），以进行后续处理。 值为**启用**意味着，可以创建 Xactset，这是默认设置。 值为**禁用**创建表示现有 xactset，但所处理的任何新的 Xactset。|  
|**xactsetjob**|是否启用 Xactset 作业以创建 Xactset。 值为**启用**意味着，定期运行 Xactset 作业以在发布服务器创建 Xactset。 值为**禁用**意味着到仅由日志读取器代理创建 Xactset 时它会轮询更改的发布服务器。|  
|**xactsetjobinterval**|两次 Xactset 作业执行之间的间隔（分钟）。|  
  
 当*propertyname*省略返回的所有可设置属性。  
  
 [**@propertyvalue** =] **'***propertyvalue***’**  
 属性设置的新值。 *propertyvalue*是**sysname**，默认值为 NULL。 当*propertyvalue*省略，则当前的设置，则返回该属性。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|propertyname|**sysname**|返回以下可以设置的发布属性：<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**属性值**|**sysname**|中的属性的当前设置**propertyname**列。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_publisherproperty**用于事务复制中使用非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 当仅*发布服务器*指定，则结果集包含所有可设置属性的当前设置。  
  
 当*propertyname*命名的属性出现在结果集中的指定。  
  
 如果指定所有参数，则属性将更改，且不返回结果集。  
  
 更改时**xactsetjobinterval**正在运行的作业的属性，您必须重新启动的作业的新间隔生效。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**分发服务器上的固定的服务器角色可以执行**sp_publisherproperty**。  
  
## <a name="see-also"></a>请参阅  
 [为 Oracle 发布服务器配置事务集作业（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
