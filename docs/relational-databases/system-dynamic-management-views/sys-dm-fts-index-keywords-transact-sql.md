---
title: "sys.dm_fts_index_keywords (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords
- sys.dm_fts_index_keywords
- sys.dm_fts_index_keywords_TSQL
- dm_fts_index_keywords_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords dynamic management function
- full-text search [SQL Server], viewing keywords
- troubleshooting [SQL Server], full-text search
ms.assetid: fce7b2a1-7e74-4769-86a8-c77c7628decd
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c36ceee298c888e71dec3b3efb34990345d292c6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmftsindexkeywords-transact-sql"></a>sys.dm_fts_index_keywords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关指定表的全文索引内容的信息。  
  
 **sys.dm_fts_index_keywords**是动态管理函数。  
  
> [!NOTE]  
>  若要查看较低级别的全文检索信息，请使用[sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)文档级的动态管理函数。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.dm_fts_index_keywords( DB_ID('database_name'), OBJECT_ID('table_name') )  
```  
  
## <a name="arguments"></a>参数  
 db_id (*database_name*)  
 调用[db_id （)](../../t-sql/functions/db-id-transact-sql.md)函数。 此函数接受数据库名称，并返回数据库 ID，其中**sys.dm_fts_index_keywords**用于查找指定的数据库。 如果*database_name*是省略，则返回当前数据库 ID。  
  
 object_id (*table_name*)  
 调用[OBJECT_ID()](../../t-sql/functions/object-id-transact-sql.md)函数。 此函数接受表名，并返回包含要检查的全文索引的表的表 ID。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**关键字**|**nvarchar(4000)**|十六进制表示形式存储于全文索引内的关键字。<br /><br /> 注意： OxFF 表示指示文件或数据集的末尾的特殊字符。|  
|**display_term**|**nvarchar(4000)**|关键字的可读格式。 这种格式是从十六进制格式派生的。<br /><br /> 注意： **display_term**值 OxFF 为"的文件结尾"。|  
|**column_id**|**int**|从中对当前关键字进行全文索引的列的 ID。|  
|**document_count**|**int**|包含当前字词的文档或行的数目。|  
  
## <a name="remarks"></a>注释  
 返回的信息**sys.dm_fts_index_keywords**可用于了解以下内容，以及其他用途：  
  
-   关键字是否为全文索引的一部分。  
  
-   有多少文档或行包含给定关键字。  
  
-   全文索引中最常见的关键字：  
  
    -   **document_count**每个*keyword_value*相比总**document_count**，0xFF 文档计数。  
  
    -   通常，最常见的关键字可能适于声明为非索引字。  
  
> [!NOTE]  
>  **Document_count**返回**sys.dm_fts_index_keywords**可能是特定文档返回的计数不太准确**sys.dm_fts_index_keywords_by_document**或**CONTAINS**查询。 这一可能的不精确估计小于 1%。 由于可能出现此不精确**document_id**可能会持续跨多个行在索引片段中，或在同一行中多次出现时，两次计数。 若要获取特定文档的更准确计数，使用**sys.dm_fts_index_keywords_by_document**或**CONTAINS**查询。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-high-level-full-text-index-content"></a>A. 显示高级全文索引内容  
 以下示例显示有关 `HumanResources.JobCandidate` 表中高级全文索引内容的信息。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords(db_id('AdventureWorks2012'), object_id('HumanResources.JobCandidate'))  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索和语义搜索动态管理视图和函数 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords_by_document (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
