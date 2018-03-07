---
title: "集 QUERY_GOVERNOR_COST_LIMIT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
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
- SET QUERY_GOVERNOR_COST_LIMIT
- SET_QUERY_GOVERNOR_COST_LIMIT_TSQL
- QUERY_GOVERNOR_COST_LIMIT
- QUERY_GOVERNOR_COST_LIMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT statement
- connections [SQL Server], overriding
- QUERY_GOVERNOR_COST_LIMIT option
- overriding connection values
ms.assetid: 3424bb44-6915-462d-a8d7-fe834af81387
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a96642c6a0dd50ccb8717e84a6defec516196d87
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="set-querygovernorcostlimit-transact-sql"></a>SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  重写当前配置**查询调控器开销限制**当前连接的值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET QUERY_GOVERNOR_COST_LIMIT value  
```  
  
## <a name="arguments"></a>参数  
 *值*  
 数值或整数值，用于指定可以运行查询的最长时间。 这些值将向下舍入为最接近的整数， 负值向上舍入为 0。 查询调控器不允许执行估计开销超过该值的任何查询。 如果指定此选项为 0（默认），将关闭查询调控器，并且允许所有查询无限期运行。  
  
 “查询开销”是指在特定硬件配置中完成查询所需的估计占用时间（秒）。  
  
## <a name="remarks"></a>注释  
 仅限于在当前连接中使用 SET QUERY_GOVERNOR_COST_LIMIT，且只在当前连接期间有效。 使用[配置查询调控器开销限制服务器配置选项](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md)选项**sp_configure**若要更改服务器范围内查询调控器开销限制值。 有关配置此选项的详细信息，请参阅[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)和[服务器配置选项 &#40;SQL server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 SET QUERY_GOVERNOR_COST_LIMIT 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
