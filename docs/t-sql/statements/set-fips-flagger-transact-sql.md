---
title: "集 FIPS_FLAGGER (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/29/2017
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
- FIPS_FLAGGER
- SET_FIPS_FLAGGER_TSQL
- FIPS_FLAGGER_TSQL
- SET FIPS_FLAGGER
dev_langs:
- TSQL
helpviewer_keywords:
- SET FIPS_FLAGGER statement
- FIPS 127-2 standard
- FIPS_FLAGGER option
ms.assetid: e82f6bee-6cf6-4061-be22-9ad2e8e9d3d6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ece506e0c34f14d827e4562b8c2fcece5de1290d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定检查是否遵从 FIPS 127-2 标准。 该标准基于 ISO 标准。 有关 SQL Server FIPS 符合性信息，请参阅[如何在 FIPS 140-2 符合标准的模式中使用 SQL Server 2016](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode)。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>参数  
  *级别*   
 对 FIPS 127-2 标准的遵从级别，将检查所有数据库操作是否达到该级别。 如果数据库操作冲突的选择，ISO 标准级别[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会生成警告。  
  
 *级别*必须是以下值之一。  
  
|值|Description|  
|-----------|-----------------|  
|ENTRY|检查是否遵从 ISO 入门级标准。|  
|FULL|检查是否遵从 ISO 完全级标准。|  
|INTERMEDIATE|检查是否遵从 ISO 中间级标准。|  
|OFF|不检查是否遵从标准。|  
  
## <a name="remarks"></a>注释  
 设置`SET FIPS_FLAGGER`设置在分析时而不是在执行或运行时。 在分析时设置意味着，如果批处理或存储的过程中存在 SET 语句，则新设置将生效，而不考虑执行代码是否实际到达该点;与`SET`语句将生效，在执行任何语句之前。 例如，即使`SET`语句不在`IF...ELSE`在执行期间，永远不会达到的语句块`SET`语句仍将生效，因为`IF...ELSE`语句块的分析。  
  
 如果`SET FIPS_FLAGGER`在存储过程中的值设置`SET FIPS_FLAGGER`完成从存储过程返回控件后恢复。 因此，`SET FIPS_FLAGGER`动态 SQL 中指定的语句没有任何影响任何动态 SQL 语句后面的语句。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
