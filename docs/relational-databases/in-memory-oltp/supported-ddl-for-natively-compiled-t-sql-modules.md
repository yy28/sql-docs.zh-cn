---
title: 本机编译的 T-SQL 模块支持的 DDL | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b6bbf7b70b716eb779611d32abcfa6ff07925a28
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551347"
---
# <a name="supported-ddl-for-natively-compiled-t-sql-modules"></a>对于本机编译的 T-SQL 模块支持的 DDL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主题列出了对于本机编译的 T-SQL 模块支持的 DDL，例如存储过程、标量 UDF、内联 TVF 和触发器。  
  
 有关功能和可用作本机编译的 T-SQL 模块一部分的 T-SQL 外围应用的信息，请参阅 [本机编译的 T-SQL 模块支持的功能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)。  
  
 有关不支持的构造的信息，请参阅 [内存中 OLTP 不支持的 Transact-SQL 构造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
 支持以下各项：  
  
-   [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [DROP PROCEDURE (Transact-SQL)](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
-   [ALTER PROCEDURE (Transact-SQL)](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
-   [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md) 和 INSERT SELECT 语句  
  
-   SCHEMABINDING 和 BEGIN ATOMIC（对于本机编译存储过程是必需的）  
  
     有关详细信息，请参阅 [Creating Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)。  
  
-   NATIVE_COMPILATION  
  
     有关详细信息，请参阅 [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md)。  
  
-   可以将参数和变量声明为 NOT NULL（仅适用于本机编译模块：本机编译存储过程和本机编译标量用户定义函数）。  
  
-   表值参数。  
  
     有关详细信息，请参阅[使用表值参数（数据引擎）](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
-   EXECUTE AS OWNER、SELF、CALLER 和用户。  
  
-   表和过程的 GRANT 和 DENY 权限。  
  
     有关详细信息，请参阅 [GRANT 对象权限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md) 和 [DENY 对象权限 (Transact-SQL)](../../t-sql/statements/deny-object-permissions-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
