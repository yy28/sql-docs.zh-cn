---
title: sp_schemafilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02e384763a6415f1de27415bf63f3159bddc394e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756055"
---
# <a name="spschemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改和显示在列出适于发布的 Oracle 表时排除的架构的相关信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>参数  
 [**@publisher** =] **'***发布服务器*****  
 是的名称的非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，无默认值。  
  
 [**@schema** =] **'***架构*****  
 是架构的名称。 *架构*是**sysname**，默认值为 NULL。  
  
 [**@operation** =] **'***操作*****  
 要对此架构采取的操作。 *操作*是**nvarchar(4)**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**add**|将指定架构添加到不适合发布的架构列表中。|  
|**删除**|从不适合发布的架构列表中删除指定架构。|  
|**帮助**|返回不适合发布的架构列表。|  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**schemaname**|**sysname**|不适合发布的架构名称。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_schemafilter**仅应该用于异类发布服务器。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**分发服务器上的固定的服务器角色可以执行**sp_schemafilter**。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
