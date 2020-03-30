---
title: SET FIPS_FLAGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f666a327db29468c5bbd91bf7106d7c6e4f61f64
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67929049"
---
# <a name="set-fips_flagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定检查是否遵从 FIPS 127-2 标准。 该标准基于 ISO 标准。 有关 SQL Server FIPS 符合性信息，请参阅[如何在 FIPS 140-2 兼容模式中使用 SQL Server 2016 ](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode)。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>参数  
 **'** *level* **'**  
 对 FIPS 127-2 标准的遵从级别，将检查所有数据库操作是否达到该级别。 如果数据库操作与选定的 ISO 标准级别冲突，则 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将生成一个警告。  
  
 level 必须为以下值之一  。  
  
|值|说明|  
|-----------|-----------------|  
|ENTRY|检查是否遵从 ISO 入门级标准。|  
|FULL|检查是否遵从 ISO 完全级标准。|  
|INTERMEDIATE|检查是否遵从 ISO 中间级标准。|  
|OFF|不检查是否遵从标准。|  
  
## <a name="remarks"></a>备注  
 `SET FIPS_FLAGGER` 的设置是在分析时设置，而不是在执行或运行时设置。 在分析时进行设置意味着：SET 语句只要出现在批处理或存储过程中即生效，与代码执行实际上是否到达该点无关；并且 `SET` 语句在任何语句执行之前生效。 例如，假设 `SET` 语句在 `IF...ELSE` 语句块中，而在执行过程中从未到达过该语句块，但由于分析了 `SET` 语句块，因此 `IF...ELSE` 语句仍生效。  
  
 如果在存储过程中设置 `SET FIPS_FLAGGER`，则从存储过程返回控制后将还原 `SET FIPS_FLAGGER` 的值。 因此，动态 SQL 中指定的 `SET FIPS_FLAGGER` 语句对动态 SQL 语句之后的任何语句无效。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
