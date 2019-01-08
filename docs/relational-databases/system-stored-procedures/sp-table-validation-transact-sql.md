---
title: sp_table_validation (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41e5f03dbe8619ca2e00d70b2c569d90f75d2d2f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211277"
---
# <a name="sptablevalidation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  返回有关表或索引视图的行数或校验和信息，或者将提供的行数或校验和信息与指定的表或索引视图进行比较。 此存储过程在发布服务器上的发布数据库中执行，或者在订阅服务器上的订阅数据库中执行。 *对 Oracle 发布服务器不支持*。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_table_validation [ @table = ] 'table'  
    [ , [ @expected_rowcount = ] type_of_check_requested OUTPUT]  
    [ , [ @expected_checksum = ] expected_checksum OUTPUT]  
    [ , [ @rowcount_only = ] rowcount_only ]  
    [ , [ @owner = ] 'owner' ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @table_name = ] table_name ]  
    [ , [ @column_list = ] 'column_list' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@table=**] **'***表*****  
 是表的名称。 *表*是**sysname**，无默认值。  
  
 [  **@expected_rowcount=**] *expected_rowcount*输出  
 指定是否返回表中的预期行数。 *expected_rowcount*是**int**，默认值为 NULL。 如果为 NULL，则将实际行数作为输出参数返回。 如果提供了一个值，则针对实际行数检查该值，以标识二者之间的差异。  
  
 [  **@expected_checksum=**] *expected_checksum*输出  
 指定是否返回表的预期校验和。 *expected_checksum*是**数值**，默认值为 NULL。 如果为 NULL，则将实际校验和作为输出参数返回。 如果提供了一个值，则针对实际校验和检查该值，以标识二者之间的差异。  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 指定要执行的校验和或行数的类型。 *type_of_check_requested*是**smallint**，默认值为**1**。  
  
 如果**0**，执行行计数和一个[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 兼容的校验和。  
  
 如果**1**，执行行计数检查。  
  
 如果**2**，执行行计数和二进制校验和。  
  
 [  **@owner=**] **'***所有者*****  
 是表的名称。 *所有者*是**sysname**，默认值为 NULL。  
  
 [  **@full_or_fast=**] *full_or_fast*  
 用于计算行计数的方法。 *full_or_fast*是**tinyint**，默认值为**2**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|使用 COUNT(*) 进行完整计数。|  
|**1**|快速从计数**sysindexes.rows**。 对行进行计数**sysindexes**比对实际表中的行计数要快得多。 但是，由于**sysindexes**是惰性更新，则 rowcount 可能不准确。|  
|**2** （默认值）|首先尝试使用快速方法进行条件性快速计数。 如果快速方法显示出差异，则转而使用完整方法。 如果*expected_rowcount*为 NULL，而且该存储的过程正在使用来获取此值，则始终使用完整 COUNT(*)。|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 如果分发代理正在执行**sp_table_validation**，指定是否在分发代理应在后立即关闭完成验证。 *shutdown_agent*是**位**，默认值为**0**。 如果**0**，复制代理不会关闭。 如果**1**、 引发错误 20578，复制代理发出信号，若要关闭的情况下。 忽略此参数时**sp_table_validation**直接由用户执行。  
  
 [  **@table_name =**] *table_name*  
 用于输出消息的视图的表名。 *table_name*是**sysname**，默认值为**@table**。  
  
 [ **@column_list**=] **'***column_list*****  
 应该在校验和函数中使用的列的列表。 *column_list*是**nvarchar(4000)**，默认值为 NULL。 启用合并项目验证，以指定不包括计算列和时间戳列的列列表。  
  
## <a name="return-code-values"></a>返回代码值  
 如果执行校验和验证并且预期校验和等于表中的校验和**sp_table_validation**返回表通过校验和验证一条消息。 否则，将返回一条消息，指示表可能不同步，并报告预期的行数和实际行数之间的差异。  
  
 如果执行行计数验证并且预期的行数等于在表中，数字**sp_table_validation**返回一条消息，表通过行计数验证。 否则，将返回一条消息，指示表可能不同步，并报告预期的行数和实际行数之间的差异。  
  
## <a name="remarks"></a>备注  
 **sp_table_validation**用于所有类型的复制。 **sp_table_validation** Oracle 发布服务器不支持。  
  
 校验和对页上的整个行图像上计算 32 位循环冗余检查 (CRC)。 它不是有选择地检查列，并且不能对视图或表的垂直分区进行操作。 此外，校验和跳过的内容**文本**并**映像**（按照设计） 的列。  
  
 执行校验和检查时，两个服务器的表结构必须完全相同；也就是说，表中包含的列必须相同，且列的顺序、数据类型和长度以及 NULL/NOT NULL 条件都必须相同。 例如，如果发布服务器执行 CREATE TABLE，然后执行 ALTER TABLE 以添加列，但是订阅服务器上应用的脚本是一个简单的 CREATE 表，则表结构不相同。 如果您不能确定两个表的结构是否相同，看看[syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) ，确认每个表中的偏移量是否相同。  
  
 浮点值很可能产生校验和差异，如果字符模式**bcp**时使用的这是这种情况，如果发布拥有非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。 这是由于在进行字符模式转换时，精度上存在不可避免的微小差异。  
  
## <a name="permissions"></a>权限  
 若要执行**sp_table_validation**，必须在正在验证的表拥有 SELECT 权限。  
  
## <a name="see-also"></a>请参阅  
 [校验和&#40;Transact SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT (Transact-SQL)](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
