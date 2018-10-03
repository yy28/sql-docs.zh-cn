---
title: sp_helpindex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpindex_TSQL
- sp_helpindex
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpindex
ms.assetid: c7f73ba0-ec35-4b10-aa5f-f1487e51fbf7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 064018cdc595935ce3987fc44bc7be7da74bbd02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727695"
---
# <a name="sphelpindex-transact-sql"></a>sp_helpindex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  报告有关表或视图索引的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpindex [ @objname = ] 'name'  
```  
  
## <a name="arguments"></a>参数  
 [ **@objname=** ] **'***name***'**  
 用户定义的表或视图的限定或非限定名称。 仅当指定限定的表或视图名称时，才需要使用引号。 如果提供的是完全限定名称（包括数据库名称），则数据库名称必须是当前数据库的名称。 *名称*是**nvarchar(776)**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**index_name**|**sysname**|索引名。|  
|**index_description**|**varchar(210)**|索引说明，其中包括索引所在的文件组。|  
|**index_keys**|**nvarchar(2078)**|对其生成索引的表或视图列。|  
  
 被降序索引的列将在结果集中列出，该列的名称后面带有一个减号 (-)，当列出被升序索引的列（这是默认情况）时，只带有该列的名称。  
  
## <a name="remarks"></a>备注  
 如果已通过使用 UPDATE STATISTICS 的 NORECOMPUTE 选项设置的索引，该信息包含在**index_description**列。  
  
 **sp_helpindex**只显示可排序的索引列; 因此，不显示关于 XML 索引或空间索引的信息。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例报告 `Customer` 表的索引类型。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpindex N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [更新统计信息 (Transact-SQL)](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
