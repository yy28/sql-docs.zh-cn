---
title: sp_table_validation (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d82517f09ad18c7cc0b2e8d49acfdae6ab200ee9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33002674"
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
 [  **@table=**] *****表*****  
 是表的名称。 *表*是**sysname**，无默认值。  
  
 [  **@expected_rowcount=**] *expected_rowcount*输出  
 指定是否返回表中的预期行数。 *expected_rowcount*是**int**，默认值为 NULL。 如果为 NULL，则将实际行数作为输出参数返回。 如果提供了一个值，则针对实际行数检查该值，以标识二者之间的差异。  
  
 [  **@expected_checksum=**] *expected_checksum*输出  
 指定是否返回表的预期校验和。 *expected_checksum*是**数值**，默认值为 NULL。 如果为 NULL，则将实际校验和作为输出参数返回。 如果提供了一个值，则针对实际校验和检查该值，以标识二者之间的差异。  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 指定要执行的校验和或行数的类型。 *type_of_check_requested*是**smallint**，默认值为**1**。  
  
 如果**0**，执行行计数和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 兼容的校验和。  
  
 如果**1**，执行行计数检查。  
  
 如果**2**，执行行计数和二进制校验和。  
  
 [  **@owner=**] *****所有者*****  
 是表的名称。 *所有者*是**sysname**，默认值为 NULL。  
  
 [  **@full_or_fast=**] *full_or_fast*  
 用于计算行计数的方法。 *full_or_fast*是**tinyint**，默认值为**2**，并且可以为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|使用 COUNT(*) 进行完整计数。|  
|**1**|未快速从计数**sysindexes.rows**。 计算行数**sysindexes**比计算实际的表中的行数快得多。 但是，因为**sysindexes**是延迟更新，则行计数可能不准确。|  
|**2** （默认值）|首先尝试使用快速方法进行条件性快速计数。 如果快速方法显示出差异，则转而使用完整方法。 如果*expected_rowcount*为 NULL，而存储的过程正在使用来获取的值，始终使用完整 COUNT(*)。|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 如果分发代理正在执行**sp_table_validation**，指定是否分发代理应立即在完成后关闭的验证。 *shutdown_agent*是**位**，默认值为**0**。 如果**0**，复制代理不会关闭。 如果**1**、 引发错误 20578 和复制代理处于有信号状态关闭。 忽略此参数时**sp_table_validation**直接由用户执行。  
  
 [  **@table_name =**] *table_name*  
 用于输出消息的视图的表名。 *table_name*是**sysname**，默认值为**@table**。  
  
 [ **@column_list**=] *****column_list*****  
 应该在校验和函数中使用的列的列表。 *column_list*是**nvarchar （4000)**，默认值为 NULL。 启用合并项目验证，以指定不包括计算列和时间戳列的列列表。  
  
## <a name="return-code-values"></a>返回代码值  
 如果执行校验和验证与预期校验和等于在表中，校验和**sp_table_validation**返回表通过校验和验证的消息。 否则，将返回一条消息，指示表可能不同步，并报告预期的行数和实际行数之间的差异。  
  
 如果执行行计数验证和预期的行数等于在表中，数**sp_table_validation**返回表传递行计数验证的消息。 否则，将返回一条消息，指示表可能不同步，并报告预期的行数和实际行数之间的差异。  
  
## <a name="remarks"></a>注释  
 **sp_table_validation**在所有类型的复制中使用。 **sp_table_validation** Oracle 发布服务器不支持。  
  
 校验和对页上的整个行图像上计算 32 位循环冗余检查 (CRC)。 它不是有选择地检查列，并且不能对视图或表的垂直分区进行操作。 此外，校验和跳过的内容**文本**和**映像**（按照设计） 的列。  
  
 执行校验和检查时，两个服务器的表结构必须完全相同；也就是说，表中包含的列必须相同，且列的顺序、数据类型和长度以及 NULL/NOT NULL 条件都必须相同。 例如，如果发布服务器执行 CREATE TABLE，然后执行 ALTER TABLE 以添加列，但是订阅服务器上应用的脚本是一个简单的 CREATE 表，则表结构不相同。 如果您不能确定两个表的结构，并完全相同，看看[syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md)并确认每个表中的偏移量是否相同。  
  
 浮点值很可能生成校验和的差异，如果字符模式**bcp**所使用的这是这种情况，如果发布具有非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。 这是由于在进行字符模式转换时，精度上存在不可避免的微小差异。  
  
## <a name="permissions"></a>权限  
 若要执行**sp_table_validation**，你必须正被验证对表具有 SELECT 权限。  
  
## <a name="see-also"></a>另请参阅  
 [校验和&#40;Transact SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT (Transact-SQL)](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
