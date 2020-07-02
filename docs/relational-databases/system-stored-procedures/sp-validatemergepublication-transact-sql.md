---
title: sp_validatemergepublication （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergepublication
- sp_validatemergepublication_TSQL
helpviewer_keywords:
- sp_validatemergepublication
ms.assetid: 5a862f1a-2be1-4758-9954-4cdc8c77d149
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd8e069c1029e2b715772b0dbcc9d0495ad0f0d4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723011"
---
# <a name="sp_validatemergepublication-transact-sql"></a>sp_validatemergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  执行整个发布范围内的验证，一次性地验证所有订阅（推送、请求和匿名）。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_validatemergepublication [@publication=] 'publication'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>自变量  
 [** \@ 发布 =**] **"***发布***"**  
 发布的名称。 *发布*为**sysname**，无默认值。  
  
`[ @level = ] level`要执行的验证的类型。 *级别*为**tinyint**，无默认值。 级别可以为下列值之一：  
  
|级别值|说明|  
|-----------------|-----------------|  
|**1**|只验证行计数。|  
|**2**|验证行计数和校验和。 对于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 订阅服务器，此设置自动设置为**3**。|  
|**3**|此为建议值。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_validatemergepublication**用于合并复制。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_validatemergepublication**执行。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [验证复制的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_validatemergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)  
  
  
