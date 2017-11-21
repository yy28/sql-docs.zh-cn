---
title: "排序规则 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9154d293ca5b7737a9c80fef0754dcec6e461a46
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="collations"></a>排序规则
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  一个子句，可应用于数据库定义或列定义以定义排序规则，或应用于字符串表达式以应用排序规则转换。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
COLLATE { <collation_name> | database_default }  
<collation_name> :: =   
     { Windows_collation_name } | { SQL_collation_name }  
```  
  
## <a name="arguments"></a>参数  
 *collation_name*  
 应用于表达式、列定义或数据库定义的排序规则的名称。 *collation_name*可以仅指定*Windows_collation_name*或*SQL_collation_name*。 *collation_name*必须是文字值。 *collation_name*不能通过变量或表达式表示。  
  
 *Windows_collation_name*是的排序规则名称[Windows 排序规则名称](../../t-sql/statements/windows-collation-name-transact-sql.md)。  
  
 *SQL_collation_name*是的排序规则名称[SQL Server 排序规则名称](../../t-sql/statements/sql-server-collation-name-transact-sql.md)。  
  
 在数据库定义级别应用排序规则时，仅 Unicode 的 Windows 排序规则不能与 COLLATE 子句一起使用。  
  
 **database_default**  
 使 COLLATE 子句继承当前数据库的排序规则。  
  
## <a name="remarks"></a>注释  
 可以在多个级别指定 COLLATE 子句。 其中包括：  
  
1.  创建或更改数据库。  
  
     可以使用 CREATE DATABASE 或 ALTER DATABASE 语句的 COLLATE 子句指定数据库的默认排序规则。 还可以在使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建数据库时指定排序规则。 如果不指定排序规则，则将为数据库分配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的默认排序规则。  
  
    > [!NOTE]  
    >  Windows 仅限 Unicode 的排序规则只能与 COLLATE 子句要应用到的排序规则**nchar**， **nvarchar**，和**ntext**在列级别上的数据类型和表达式级数据;它们不能与 COLLATE 子句来更改数据库或服务器实例的排序规则。  
  
2.  创建或更改表列。  
  
     可以使用 CREATE TABLE 或 ALTER TABLE 语句的 COLLATE 子句指定每个字符串列的排序规则。 还可以在使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建表时指定排序规则。 如果不指定排序规则，将为列分配数据库的默认排序规则。  
  
     你还可以使用`database_default`COLLATE 子句中的选项以指定临时表中的列，而不是连接使用的当前用户数据库的默认排序规则**tempdb**。  
  
3.  转换表达式的排序规则。  
  
     可以使用 COLLATE 子句将字符表达式应用于某个排序规则。 为字符文本和变量分配当前数据库的默认排序规则。 为列引用分配列的定义排序规则。  
  
 标识符的排序规则取决于定义标识符的级别。 为实例级对象（如登录名和数据库名）的标识符分配实例的默认排序规则。 为数据库对象（如表、视图和列名）的标识符分配数据库的默认排序规则。 例如，对于名称差别仅在于大小写的两个表，可在使用区分大小写排序规则的数据库中创建，而不能在使用不区分大小写排序规则的数据库中创建。 有关详细信息，请参阅 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)。  
  
 当连接上下文与某个数据库相关时，可以创建变量、GOTO 标签、临时存储过程和临时表，且当已将上下文切换到其他数据库时引用它们。 变量、GOTO 标签、临时存储过程和临时表的标识符位于服务器实例的默认排序规则中。  
  
 COLLATE 子句可以应用于仅**char**， **varchar**，**文本**， **nchar**， **nvarchar**和**ntext**数据类型。  
  
 COLLATE 使用*collate_name*来指代的 SQL Server 排序规则或要应用于表达式、 列定义或数据库定义的 Windows 排序规则的名称。 *collation_name*可以仅指定*Windows_collation_name*或*SQL_collation_name*和该参数必须包含一个文本值。 *collation_name*不能通过变量或表达式表示。  
  
 排序规则一般由排序规则名称标识，安装过程中除外。 在安装过程中，您应该为 Windows 排序规则指定根排序规则指示符（排序规则区域设置），然后指定区分或不区分大小写或重音的排序选项。  
  
 你可以执行系统函数[fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)若要检索的 Windows 排序规则和 SQL Server 排序规则的所有有效的排序规则名称的列表：  
  
```  
SELECT name, description  
FROM fn_helpcollations();  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只支持由基础操作系统支持的代码页。 在执行取决于排序规则的操作时，引用的对象所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则必须使用计算机上运行的操作系统所支持的代码页。 这些操作可能包括：  
  
-   当创建或更改数据库时，为数据库指定默认排序规则。  
  
-   当创建或更改表时，为列指定排序规则。  
  
-   当还原或附加数据库、 数据库的默认排序规则和任何的排序规则**char**， **varchar**，和**文本**列或数据库中的参数必须由操作系统支持。  
  
     支持代码页转换**char**和**varchar**数据类型，但不是能为**文本**数据类型。 不报告代码页转换过程中的数据丢失。  
  
 如果指定的排序规则或者被引用的对象使用的排序规则使用 Windows，不支持代码页[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]显示错误。  
  
## <a name="examples"></a>示例  
  
### <a name="a-specifying-collation-during-a-select"></a>A. 在选择过程中指定排序规则  
 下面的示例创建一个简单表并插入 4 行。 然后，该示例在从表中选择数据时应用了两个排序规则，演示 `Chiapas` 如何以不同方式排序。  
  
```tsql  
CREATE TABLE Locations  
(Place varchar(15) NOT NULL);  
GO  
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')  
                             , ('Cinco Rios'), ('California');  
GO  
--Apply an typical collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Latin1_General_CS_AS_KS_WS ASC;  
GO  
-- Apply a Spanish collation  
SELECT Place FROM Locations  
ORDER BY Place  
COLLATE Traditional_Spanish_ci_ai ASC;  
GO  
```  

 这里是第一个查询的结果。  
  
 ```
 Place 
 ------------- 
 California 
 Chiapas 
 Cinco Rios 
 Colima
 ```  
  
 这里是第二个查询的结果。  
  
 ```
 Place 
 ------------- 
 California 
 Cinco Rios 
 Colima 
 Chiapas
 ```  
  
### <a name="b-additional-examples"></a>B. 其他示例  
 有关使用的其他示例**COLLATE**，请参阅[CREATE DATABASE &#40;SQL Server Transact SQL &#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)示例**G.创建数据库并指定排序规则名称和选项**，和[ALTER TABLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md)示例**V.更改列排序规则**。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)   
 [排序规则优先级 (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [常量 &#40;Transact SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [table &#40;Transact SQL &#41;](../../t-sql/data-types/table-transact-sql.md)  
  
  

