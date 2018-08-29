---
title: sp_estimated_rowsize_reduction_for_vardecimal (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- sp_estimated_rowsize_reduction_for_vardecimal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- decimal data type, compressing
- numeric data type, compressing
- estimate decimal compression
- table compression [SQL Server]
ms.assetid: 0fe45983-f9f2-4c7f-938a-0fd96e1cbe8d
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2b82d06ba4e6bc8927fca7edd807c98e595ea93d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43022147"
---
# <a name="spestimatedrowsizereductionforvardecimal-transact-sql"></a>sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  估计对表启用 vardecimal 存储格式后行平均大小的减少量。 使用该数字可估计表大小的总体减少量。 由于使用统计采样来计算行大小的平均减少量，因此只能将该计算结果视为估计值。 在极个别的情况下，启用 vardecimal 存储格式后行大小可能会增加。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用 ROW 和 PAGE 压缩。 有关详细信息，请参阅 [Data Compression](../../relational-databases/data-compression/data-compression.md)。 有关对表和索引的大小的压缩效果，请参阅[sp_estimate_data_compression_savings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_estimated_rowsize_reduction_for_vardecimal [ [ @table_name = ] 'table'] [;]  
```  
  
## <a name="arguments"></a>参数  
 [  **@table=** ] **'***表*****  
 由三部分组成的表名，将要更改此表的存储格式。 *表*是**nvarchar(776)**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 将返回如下结果集，以提供当前表大小和估计表大小的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**avg_rowlen_fixed_format**|**十进制 （12、 2）**|以固定十进制存储格式表示行的长度。|  
|**avg_rowlen_vardecimal_format**|**十进制 （12、 2）**|表示使用 vardecimal 存储格式时的平均行大小。|  
|**row_count**|**int**|表中的行数。|  
  
## <a name="remarks"></a>Remarks  
 使用**sp_estimated_rowsize_reduction_for_vardecimal**来估计如果启用了 vardecimal 存储格式的表的存储。 例如，如果平均行大小能够减少 40%，则可能可以将表的大小减少 40%。 您可能无法节省空间，具体取决于填充因子和行大小。 例如，如果某行长度为 8000 字节并且您将该行的大小减少 40%，则数据页上仍只能容纳一行，因而并未节省空间。  
  
 如果结果**sp_estimated_rowsize_reduction_for_vardecimal**指示表将增长，这意味着表中的许多行使用几乎 decimal 数据类型的完全精度和增加的少量vardecimal 存储格式所需的开销大于 vardecimal 存储格式的节省。 在这种极个别的情况下，不要启用 vardecimal 存储格式。  
  
 如果对表启用 vardecimal 存储格式，使用**sp_estimated_rowsize_reduction_for_vardecimal**来估计在禁用了 vardecimal 存储格式的行的平均大小。  
  
## <a name="permissions"></a>Permissions  
 需要对表具有 CONTROL 权限。  
  
## <a name="examples"></a>示例  
 下例估计了 `Production.WorkOrderRouting` 数据库中的 `AdventureWorks2012` 表在压缩后行大小变小的情况。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimated_rowsize_reduction_for_vardecimal 'Production.WorkOrderRouting' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_db_vardecimal_storage_format &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)   
 [sp_tableoption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
