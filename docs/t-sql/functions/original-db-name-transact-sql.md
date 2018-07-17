---
title: ORIGINAL_DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ORIGINAL_DB_NAME
- ORIGINAL_DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ORIGINAL_DB_NAME function
ms.assetid: 7dadc40a-1287-4f31-8487-434ee477144d
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec192d9d148492e9fb3d19fd9858b92c36024881
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783274"
---
# <a name="originaldbname-transact-sql"></a>ORIGINAL_DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回由用户在数据库连接字符串中指定的数据库名称。 这是使用 sqlcmd-d 选项 (USE database) 或 ODBC 数据源表达式（initial catalog = 数据库名称）指定的数据库。  
  
 该数据库与默认用户数据库不同。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ORIGINAL_DB_NAME ()  
```  
  
## <a name="remarks"></a>Remarks  
 如果未指定初始数据库，则该函数将返回一个空字符串。  
  
## <a name="see-also"></a>另请参阅  
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)   
 [osql 实用工具](../../tools/osql-utility.md)   
 [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
