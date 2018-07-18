---
title: COL_LENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1ec5148b6a497efe10daf2a8b88c3862dc20e95f
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37787648"
---
# <a name="collength-transact-sql"></a>COL_LENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函数返回定义的列长度（以字节为单位）。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>参数  
**'** table **'**  
要确定其列长度信息的表的名称。 table 是 nvarchar 类型的表达式。
  
' column '  
要确定其长度的列名称。 column 是 nvarchar 类型的表达式。
  
## <a name="return-type"></a>返回类型
**int**
  
## <a name="exceptions"></a>异常  
出现错误时或调用方没有查看对象的正确权限时将返回 NULL。
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，用户只能查看其所拥有的安全对象的元数据，或者已对其授予权限的安全对象的元数据。 这意味着，如果用户对该对象没有正确的权限，那些发出元数据的内置函数（如 COL_LENGTH）则可能会返回 NULL。 有关详细信息，请参阅[元数据可见性配置](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>Remarks  
对于使用 max 说明符 (varchar(max)) 声明的 varchar 列，COL_LENGTH 将返回值 –1。
  
## <a name="examples"></a>示例  
此示例将显示类型为 `varchar(40)` 和 `nvarchar(40)` 的列的返回值：
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 varchar(40), c2 nvarchar(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>另请参阅
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME (Transact-SQL)](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY (Transact-SQL)](../../t-sql/functions/columnproperty-transact-sql.md)
  
  
