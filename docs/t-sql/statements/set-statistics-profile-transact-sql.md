---
title: SET STATISTICS PROFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5675050352b26dd0fb3a017891563070c97473c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655577"
---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  显示语句的配置文件信息。 STATISTICS PROFILE 对即席查询、视图和存储过程有效。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 STATISTICS PROFILE 为 ON 时，执行的各个查询都返回其常规结果集，后面跟一个附加结果集，显示查询执行的配置文件。  
  
 附加结果集包含查询的 SHOWPLAN_ALL 列以及下面的附加列。  
  
|列名|描述|  
|-----------------|-----------------|  
|**行**|各运算符生成的实际行数|  
|**Executes**|运算符执行的次数|  
  
## <a name="permissions"></a>Permissions  
 若要使用 SET STATISTICS PROFILE 并查看输出，用户必须拥有下列权限：  
  
-   执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的相应权限。  
  
-   对包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句引用的对象的所有数据库有 SHOWPLAN 权限。  
  
 对于不生成 STATISTICS PROFILE 结果集的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，只需具有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的相应权限。 对于生成 STATISTICS PROFILE 结果集的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，请确保既有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句执行权限又有 SHOWPLAN 权限，否则会中止执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，而 Showplan 信息也不会生成。  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL (Transact-SQL)](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME (Transact-SQL)](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS TIME (Transact-SQL)](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
