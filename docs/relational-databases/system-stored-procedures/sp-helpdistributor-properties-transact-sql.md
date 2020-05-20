---
title: sp_helpdistributor_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_properties_TSQL
- sp_helpdistributor_properties
helpviewer_keywords:
- sp_helpdistributor_properties
ms.assetid: ee267724-3244-49eb-84c9-f38dbefdd639
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c3c044f9cd63f5942fdc212b2321628ac1b2c21
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828922"
---
# <a name="sp_helpdistributor_properties-transact-sql"></a>sp_helpdistributor_properties (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  返回分发服务器属性。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdistributor_properties   
```  
  
## <a name="result-set"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**heartbeat_interval**|**int**|在不记录进度消息的情况下，代理可以运行的最大分钟数。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helpdistributor_properties**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员、分发数据库上**db_owner**或**replmonitor**固定数据库角色的成员，以及使用此分发服务器的发布的发布访问列表（PAL）中的用户才能执行**sp_helpdistributor_properties**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_changedistributor_property &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)  
  
  
