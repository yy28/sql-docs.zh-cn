---
description: sp_execute (Transact-SQL)
title: sp_execute (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49b5548d149640b7e9d78b38c70c22fd6c5ae163
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005607"
---
# <a name="sp_execute-transact-sql"></a>sp_execute (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)]使用指定的句柄和可选参数值执行已准备的语句。 通过在表格格式数据流 (TDS) 数据包中指定 ID = 12 来调用 sp_execute。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure Synapse Analytics, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>参数  
 *柄*  
 Sp_prepare 返回的 *句柄* 值。 *句柄* 是一个参数，它需要调用 **int** 输入值。  
  
 *bound_param*  
 指示使用其他参数。 *bound_param* 是必需的参数，该参数调用任意数据类型的输入值来表示过程的附加参数。  
  
> [!NOTE]  
>  *bound_param*必须与 sp_prepare*参数*值所进行的声明相匹配，并且可以采用* @name = 值*或*值*形式。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_prepare &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  
