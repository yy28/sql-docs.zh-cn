---
title: sp_fulltext_pendingchanges (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 05f6b48dff75a1dd6bb11cd615d02306c2f7eeee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spfulltextpendingchanges-transact-sql"></a>sp_fulltext_pendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  针对正在使用更改跟踪的指定表返回未处理的更改，例如挂起的插入、更新和删除。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>参数  
 *table_id*  
 表的 ID。 如果该表未进行全文索引，或未对该表启用更改跟踪，则将返回错误。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**Key**|*|指定表中的全文键值。|  
|**DocId**|**bigint**|与键值相对应的内部文档标识符 (DocId) 列。|  
|**状态**|**int**|0 = 将从全文索引中删除行。<br /><br /> 1 = 将对行进行全文索引。<br /><br /> 2 = 行是最新的。<br /><br /> -1 = 行处于过渡（进行了批处理，但未提交）状态或错误状态。|  
|**DocState**|**tinyint**|内部文档标识符 (DocId) 映射状态列的原始转储。|  
  
 <sup>* 相同基表中的全文键列的数据类型是密钥的数据类型。</sup>  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="remarks"></a>注释  
 如果没有要处理的更改，则返回一个空行集。  
  
 全文搜索查询不会返回的行**状态**值为 0。 这是因为该行已从基表中删除且正等待从全文索引中删除。  
  
 若要了解多少处更改处于挂起状态对于特定的表，使用**TableFullTextPendingChanges** OBJECTPROPERTYEX 函数属性。  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索和语义搜索存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX (Transact-SQL)](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
