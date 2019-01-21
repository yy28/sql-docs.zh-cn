---
title: SET ANSI_DEFAULTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 871d79c805451e1710dbc400914d2dace01c7eea
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143437"
---
# <a name="set-ansidefaults-transact-sql"></a>SET ANSI_DEFAULTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  控制一组可共同指定某种 ISO 标准行为的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>语法

```
-- Syntax for SQL Server

SET ANSI_DEFAULTS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_DEFAULTS ON
```

## <a name="remarks"></a>Remarks  
ANSI_DEFAULTS 是客户端不会修改的服务器端设置。 客户端管理自己的设置。 在默认情况下，这些设置与服务器设置相反。 用户不应修改服务器设置。 若要更改客户端行为，用户应使用 SQL_COPT_SS_PRESERVE_CURSORS。 有关详细信息，请参阅 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
当启用 (ON) 时，此选项将启用下列 ISO 设置：  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
这些 ISO 标准 SET 选项共同定义了用户工作会话、运行触发器或存储过程执行期间的查询处理环境。 不过，这些 SET 选项并未包括遵守 ISO 标准所需的所有选项。  
  
在处理计算列和索引视图上的索引时，必须将这四个默认选项（ANSI_NULLS、ANSI_PADDING、ANSI_WARNINGS 和 QUOTED_IDENTIFIER）设置为 ON。 这些默认选项是七个 SET 选项中的一部分，当您在计算列和索引视图上创建和更改索引时，必须给这七个选项分配必需的值。 另外三个 SET 选项分别是：ARITHABORT (ON)、CONCAT_NULL_YIELDS_NULL (ON) 和 NUMERIC_ROUNDABORT (OFF)。 有关计算列上的索引视图和索引所必需的 SET 选项设置的详细信息，请参阅[使用 SET 语句时的注意事项](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序在连接时会自动将 ANSI_DEFAULTS 设置为 ON。 然后，驱动程序和访问接口将 CURSOR_CLOSE_ON_COMMIT 和 IMPLICIT_TRANSACTIONS 设置为 OFF。 CURSOR_CLOSE_ON_COMMIT 和 IMPLICIT_TRANSACTIONS 的 OFF 设置可以在 ODBC 数据源、ODBC 连接属性或 OLE DB 连接属性（它们在连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前在应用程序中进行设置）中进行配置。 对于 DB-Library 应用程序的连接，ANSI_DEFAULTS 默认为 OFF。  
  
当发出 SET ANSI_DEFAULTS 时，QUOTED_IDENTIFIER 将在分析时进行设置，而下列选项则在执行时进行设置：  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>Permissions  
要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
以下示例将 ANSI_DEFAULTS 设置为 ON，并使用 `DBCC USEROPTIONS` 语句显示受影响的设置。  
  
```sql  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  

-- Display the current settings.  
DBCC USEROPTIONS;  
GO 

-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DBCC USEROPTIONS (Transact-SQL)](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON (Transact-SQL)](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS (Transact-SQL)](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING (Transact-SQL)](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS (Transact-SQL)](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL)](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS (Transact-SQL)](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
