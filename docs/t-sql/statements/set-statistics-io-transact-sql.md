---
title: "设置 STATISTICS IO (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_IO_TSQL
- IO
- IO_TSQL
- SET STATISTICS IO
dev_langs:
- TSQL
helpviewer_keywords:
- disk I/O statistics [SQL Server]
- I/O [SQL Server], disk activity information
- disks [SQL Server], statement statistics
- STATISTICS IO option
- statements [SQL Server], statistical information
- SET STATISTICS IO statement
- statistical information [SQL Server], disk activity
ms.assetid: 7033aac9-a944-4156-9ff4-6ef65717a28b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3b2aad11610a23c3686e279daa60c57bf7c8154f
ms.sourcegitcommit: b09bccd6dfdba55b022355e892c29cb50aadd795
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2018
---
# <a name="set-statistics-io-transact-sql"></a>SET STATISTICS IO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 显示有关由 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句生成的磁盘活动量的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET STATISTICS IO { ON | OFF }  
```  
  
## <a name="remarks"></a>注释  
 如果 STATISTICS IO 为 ON，则显示统计信息。 如果为 OFF，则不显示统计信息。  
  
 如果将此选项设置为 ON，则所有后续的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句将返回统计信息，直到将该选项设置为 OFF 为止。  
  
 下表列出并说明了各个输出项。  
  
|输出项|含义|  
|-----------------|-------------|  
|**表**|表的名称。|  
|**扫描计数**|在任何方向都达到叶级别后启动的查询/扫描数，目的在于检索用于构造输出的最终数据集的所有值。<br /><br /> 如果使用的索引是主键的唯一索引或聚集索引并且您仅查找一个值，则扫描计数为 0。 例如 `WHERE Primary_Key_Column = <value>`。<br /><br /> 使用非唯一聚集的索引非主键列上定义的一个值搜索时，扫描计数为 1。 这是为了针对您正在搜索的键值检查重复值。 例如 `WHERE Clustered_Index_Key_Column = <value>`。<br /><br /> 当 N 为通过使用索引键定位键值后，在叶级别的左侧或右侧启动的不同查找/扫描数时，则扫描计数为 N。|  
|**逻辑读取次数**|从数据缓存读取的页数。|  
|**物理读取次数**|从磁盘读取的页数。|  
|**预读次数**|为进行查询而放入缓存的页数。|  
|**lob 逻辑读取次数**|数**文本**， **ntext**，**映像**，或较大的值类型 (**varchar （max)**， **nvarchar (max)**，**varbinary （max)**) 从数据缓存中读取页。|  
|**lob 物理读取次数**|数**文本**， **ntext**，**映像**或从磁盘读取较大的值类型页。|  
|**lob 预读读取次数**|数**文本**， **ntext**，**映像**或较大的值类型放入缓存中用于查询的页。|  
  
 SET STATISTICS IO 是在执行或运行时设置，而不是在分析时设置。  
  
> [!NOTE]  
>  当 Transact-SQL 语句检索 LOB 列时，有些 LOB 检索操作可能需要多次遍历 LOB 树。 这可能会导致 SET STATISTICS IO 报告的次数比预期的逻辑读取次数更高。  
  
## <a name="permissions"></a>权限  
 若要使用 SET STATISTICS IO，用户必须具有执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的适当权限。 但不需要 SHOWPLAN 权限。  
  
## <a name="examples"></a>示例  
 此示例显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理语句时，进行了多少次逻辑读和物理读操作。  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS IO ON;  
GO  
SELECT *   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS IO OFF;  
GO  
```  
  
 下面是结果集：  
  
```  
Table 'ProductCostHistory'. Scan count 1, logical reads 5, physical   
reads 0, read-ahead reads 0, lob logical reads 0, lob physical reads 0,   
lob read-ahead reads 0.  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [设置 SHOWPLAN_ALL &#40;Transact SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [设置统计信息时间 &#40;Transact SQL &#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)  
  
  
