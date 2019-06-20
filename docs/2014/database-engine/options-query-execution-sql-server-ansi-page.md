---
title: 选项 （查询执行 SQL Server ANSI 页） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAnsi
ms.assetid: 0f4c6887-0562-417e-806c-b5cffb1e7c5c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e075de106a66ffee63c02ead06a3fc68548111a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089381"
---
# <a name="options-query-execution-sql-server-ansi-page"></a>选项 （查询执行 SQL Server ANSI 页）
  这些 ANSI (ISO) 标准 SET 选项共同定义了用户查询、运行触发器或存储过程执行期间的查询处理环境。 不过，这些 SET 选项并未包括遵守 ISO 标准所需的所有选项。 使用此页可以指定 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用 ISO 标准中指定的全部或部分设置运行查询。 对这些选项所做的更改只应用于新的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询。 若要更改当前查询的选项，请在“查询”  菜单上单击“查询选项”  ，或在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查询窗口中单击右键，再选择“查询选项”  。 在 **“查询选项”** 对话框中的 **“执行”** 下，单击 **ANSI**。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **SET ANSI_DEFAULTS**  
 选中此复选框可以选择所有默认的 ISO 设置。 默认情况下，不会选择所有 ISO 选项。  
  
 **SET QUOTED_IDENTIFIER**  
 如果选中此复选框，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将遵从有关引号分隔标识符和文字字符串的 ISO 规则。 由引号分隔的标识符可以是 Transact-SQL 保留关键字，也可以包含 Transact-SQL 标识符语法规则通常不允许的字符。 默认情况下，此复选框为选中状态。  
  
 **SET ANSI_NULL_DFLT_ON**  
 当设置了此值时，在 CREATE TABLE 或 ALTER TABLE 语句执行过程中，没有显式定义为 NOT NULL 的所有用户定义的数据类型或列都将默认为允许空值。 默认情况下，此复选框为选中状态。  
  
 **SET IMPLICIT_TRANSACTIONS**  
 如果选中此复选框，则 SET IMPLICIT_TRANSACTIONS 将连接设置为隐式事务模式。 如果清除此复选框，则会将连接返回到自动提交事务模式。 若要查看在选中此复选框时可启动隐式事务的语句，请参阅 [SET IMPLICIT_TRANSACTIONS (Transact-SQL)](/sql/t-sql/statements/set-implicit-transactions-transact-sql)。 默认情况下，此复选框处于未选中状态。  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 如果选中此复选框，则在提交事务时，所有打开的游标都将自动关闭（符合 ISO 标准）。 当此值设置为 OFF 时，游标仍然在各事务边界间保持打开状态，并且仅当连接关闭或被显式关闭时，才会关闭游标。 默认情况下，此复选框处于未选中状态。  
  
 **SET ANSI_PADDING**  
 对于长度小于列定义大小的值名称，以及在 **char**、 **varchar**、 **binary**和 **varbinary** 数据中含有尾随空格的值，对列存储这些值名称和值的方式进行控制。 此设置只影响新列的定义。 创建列后， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 会基于创建列时的设置存储这些值。 以后对此设置的更改不会影响现有的列。 默认情况下，此复选框为选中状态。  
  
 **SET ANSI_WARNINGS**  
 指定对几种错误条件采用 ISO 标准行为：  
  
-   选中此复选框后，如果在聚合函数（如 SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP 或 COUNT）中出现了空值，则会生成一条警告消息。 当设置为 OFF 时，不发出警告。  
  
-   如果清除此复选框，则在发生被零除错误和算术溢出错误时，将导致语句回滚并生成一条错误信息。 如果设置为 OFF，则在发生被零除错误和算术溢出错误时，将导致返回空值。 如果尝试对 **character**、**Unicode** 或 **binary** 列执行 INSERT 或 UPDATE 操作，而这些列中的新值长度超出列的最大大小，那么，在发生被零除错误或算术溢出错误时，将导致返回空值。 如果 SET ANSI_WARNINGS 为 ON，则根据 ISO 标准，将取消 INSERT 或 UPDATE 操作。 字符列的尾随空格和二进制列的尾随零都将被忽略。 设置为 OFF 时，数据将剪裁为列的大小，并且语句执行成功。  
  
 默认情况下，此复选框为选中状态。  
  
 **SET ANSI_NULLS**  
 -   指定在与 Null 值一起使用等于 (=) 和不等于 (<>) 比较运算符时采用符合 ISO 标准的行为。 当选中 SET ANSI_NULLS 时，所有与 Null 值进行比较求得的值均为 UNKNOWN，这是符合 ISO 标准的行为。 如果未选中 SET ANSI_NULLS，则所有数据与空值的比较求得的值为 TRUE。 默认情况下，此复选框为选中状态。  
  
 重置为默认值   
 将此页上的所有值重置为原始默认值。  
  
  
