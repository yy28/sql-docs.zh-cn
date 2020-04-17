---
title: 在 SQL 服务器中注册用户定义类型 |微软文档
description: 在 SQL 服务器中安装 UDT 之前，必须注册 UDT。 您必须注册程序集，并在数据库中创建要使用的类型。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
author: rothja
ms.author: jroth
ms.openlocfilehash: e4383e245048035d4c05f7be3bedb7d3d13f835d
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486906"
---
# <a name="registering-user-defined-types-in-sql-server"></a>在 SQL Server 中注册用户定义类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  为了在 中使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户定义的类型 （UDT）， 必须注册它。 注册一个 UDT 涉及两个步骤：在要使用它的数据库中注册程序集和创建该类型。 UDT 的作用域仅限单个数据库，不能在多个数据库中使用，除非在各个数据库中注册相同的程序集和 UDT。 一旦注册 UDT 程序集并创建了该类型，即可在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和客户端代码中使用 UDT。 有关详细信息，请参阅 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
## <a name="using-visual-studio-to-deploy-udts"></a>使用 Visual Studio 部署 UDT  
 部署 UDT 的最简单方法是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio。 不过，对于更为复杂的部署方案，同时为尽量提高灵活性，应使用本主题下文介绍的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 遵照以下步骤使用 Visual Studio 创建和部署 UDT：  
  
1.  在**可视化基本**或**可视化 C++** 语言节点中创建新的**数据库**项目。  
  
2.  向将要包含该 UDT 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库添加引用。  
  
3.  添加**用户定义的类型**类。  
  
4.  编写用于实现该 UDT 的代码。  
  
5.  在 **"生成"** 菜单中，选择 **"部署**"。 这样即可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中注册该程序集并创建该类型。  

## <a name="using-transact-sql-to-deploy-udts"></a>使用 Transact-SQL 部署 UDT  
 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 语法可以在您希望使用 UDT 的数据库中注册程序集。 该程序集存储在内部的数据库系统表中，而不是存储在外部的文件系统中。 如果 UDT 依赖于外部程序集，则必须将这些程序集也加载到数据库中。 使用 CREATE TYPE 语句可以在要使用 UDT 的数据库中创建该 UDT。 有关详细信息，请参阅[创建"转换-SQL&#41;&#40;和](../../t-sql/statements/create-assembly-transact-sql.md)[创建类型&#40;转算-SQL&#41;。 ](../../t-sql/statements/create-type-transact-sql.md)  
  
### <a name="using-create-assembly"></a>使用 ASSEMBLY  
 使用 CREATE ASSEMBLY 语法可以在要使用 UDT 的数据库中注册程序集。 经过注册的程序集不具有任何依赖关系。  
  
 不允许在给定数据库中创建同一程序集的多个版本。 不过，可以基于给定数据库的区域性创建同一程序集的多个版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中注册的不同程序集名称来区分程序集的多个区域性版本。 有关详细信息，请参阅 .NET Framework SDK 中的“创建和使用具有强名称的程序集”。  
  
 在权限集设置为 SAFE 或 EXTERNAL_ACCESS 的情况下执行 CREATE ASSEMBLY 时，将检查程序集，确保其可验证并且是类型安全的。 如果未指定权限集，则假定为 SAFE。 不检查权限集为 UNSAFE 的代码。 有关程序集的权限集的详细信息，请参阅[设计程序集](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
#### <a name="example"></a>示例  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句使用 SAFE 权限集在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **AdventureWorks**数据库中注册 Point 程序集。 如果省略 WITH PERMISSION_SET 子句，将使用 SAFE 权限集注册该程序集。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句使用 FROM 子句中 *<assembly_bits>* 参数来注册程序集。 此**varbinary**值将文件表示为字节流。  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 ... 21ac78  
```  
  
### <a name="using-create-type"></a>使用 CREATE TYPE  
 一旦将程序集加载到数据库中，随后即可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE 语句创建该类型。 这样即可将该类型添加到该数据库的可用类型列表中。 该类型的作用域为数据库，并且只能在创建该类型的数据库中使用。 如果数据库中已存在 UDT，CREATE TYPE 语句将失败，并且生成错误。  
  
> [!NOTE]  
>  CREATE TYPE 语法还用于创建本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]别名数据类型，旨在替换**sp_addtype**作为创建别名数据类型的方法。 CREATE TYPE 语法中的某些可选参数与创建 UDT 有关，不适用于创建别名数据类型（如基类型）。  
  
 有关详细信息，请参阅[创建类型&#40;交易-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)。  
  
#### <a name="example"></a>示例  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句创建**点**类型。 外部名称是使用*程序集名称*的两部分命名语法指定的。*UDT名称*。  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>从数据库中删除 UDT  
 使用 DROP TYPE 语句从当前数据库中删除 UDT。 删除了 UDT 之后，可使用 DROP ASSEMBLY 语句从数据库中删除程序集。  
  
 在以下情况下不执行 DROP TYPE 语句。  
  
-   数据库中的表包含使用 UDT 定义的列。  
  
-   在数据库中使用 WITH SCHEMABINDING 子句创建了使用 UDT 变量或参数的函数、存储过程或触发器。  
  
### <a name="example"></a>示例  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 必须按以下顺序执行。 首先，必须删除引用**点**UDT 的表，然后删除类型，最后删除程序集。  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>查找 UDT 依赖关系  
 如果存在依赖对象，如具有 UDT 列定义的表，DROP TYPE 语句将失败。 如果存在在数据库中用 WITH SCHEMABINDING 子句创建的函数、存储过程或触发器，且这些例程使用用户定义类型的变量或参数，该语句也将失败。 在执行 DROP TYPE 语句之前，首先必须删除所有依赖对象。  
  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]查询定位**在 AdventureWorks**数据库中使用 UDT 的所有列和参数。  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>维护 UDT  
 尽管可以更改 UDT 所基于的程序集，但是一旦在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中创建了该 UDT 就无法再修改它。 多数情况下，必须使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP TYPE 语句从数据库中删除 UDT、更改基础程序集，然后使用 ALTER ASSEMBLY 语句重新加载它。 随后还需要重新创建该 UDT 和所有依赖对象。  
  
### <a name="example"></a>示例  
 在更改 UDT 程序集中的源代码并且重新编译该程序集后，可以使用 ALTER ASSEMBLY 语句。 该语句将 .dll 文件复制到服务器，并且重新绑定到新程序集。 有关完整的语法，请参阅[ALTER ASSEMBLY &#40;转算-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)。  
  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 语句从指定的磁盘位置重新加载 Point.dll 程序集。  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>使用 ALTER ASSEMBLY 添加源代码  
 CREATE ASSEMBLY 中不存在 ALTER ASSEMBLY 语法中的 ADD FILE 子句。 您可以使用该子句来添加源代码或与程序集关联的任何其他文件。 这些文件将从其原始位置复制并存储到数据库的系统表中。 如果您需要重新创建或记录 UDT 的当前版本，这样可确保源代码或其他文件随时备用。  
  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]ALTER ASSEMBLY 语句添加**点**UDT 的Point.cs类源代码。 这会复制 Point.cs 文件中包含的文本并用名称“PointSource”将其存储在数据库中。  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 程序集信息存储在已安装程序集的数据库中的**sys.assembly_files**表中。 **sys.assembly_files**表包含以下列。  
  
 **assembly_id**  
 为程序集定义的标识符。 此编号分配到与同一程序集相关的所有对象。  
  
 name   
 对象的名称。  
  
 **file_id**  
 标识每个对象的数字，第一个与给定**assembly_id**关联的对象被给定值为 1。 如果有多个对象与同一**个assembly_id，** 则每个后续**file_id**值将递增 1。  
  
 **content**  
 程序集或文件的十六进制表示形式。  
  
 您可以使用 CAST 或 CONVERT 函数将**内容**列的内容转换为可读文本。 以下查询将 Point.cs 文件的内容转换为可读文本，查询中使用 WHERE 子句中的名称将结果集限定为一行。  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 如果将结果复制并粘贴到某一文本编辑器中，您将看到原件中的换行符和空格均得到保留。  
  
## <a name="managing-udts-and-assemblies"></a>管理 UDT 和程序集  
 对 UDT 的实现进行计划时，应考虑 UDT 程序集本身所需的方法，以及应该在单独的程序集中创建并作为用户定义函数或存储过程实现的方法。 通过将方法分开放入不同的程序集，您可以更新代码，而不会影响可能存储在表的 UDT 列中的数据。 仅当新定义可以读取以前值并且类型签名未更改时，才可以修改 UDT 程序集，而无需删除 UDT 列和其他依赖对象。  
  
 将可能发生更改的过程代码与实现 UDT 所需的代码分开，可以极大地简化维护工作。 仅包括启用 UDT 所需的代码并且尽量简化 UDT 定义，这将降低出于代码修订或修复错误的目的可能需要从数据库中删除 UDT 本身的风险。  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>Currency UDT 和货币转换函数  
 **AdventureWorks**示例数据库中**的货币**UDT 提供了一个有用的示例，用于建议如何构建 UDT 及其相关功能。 **货币**UDT 用于根据特定区域性的货币系统处理货币，并允许存储不同的货币类型，如美元、欧元等。 UDT 类将区域性名称公开为字符串，并将金额公开为**小数数据类型**。 所有必需的序列化方法都包括在定义该类的程序集中。 实现从一个区域性到另一个区域性的货币转换的函数作为名为**ConvertCurrency**的外部函数实现，并且此函数位于单独的程序集中。 **ConvertCurrency**函数通过从**AdventureWorks**数据库中的表检索转换率来执行其工作。 如果转换速率的来源应该更改，或者如果对现有代码应进行任何其他更改，则可以轻松地修改程序集，而不会影响**货币**UDT。  
  
 可以通过安装通用语言运行时 （CLR） 示例找到**货币**UDT 和**ConvertCurrency**函数的代码列表。  
  
### <a name="using-udts-across-databases"></a>跨数据库使用 UDT  
 根据定义，UDT 的作用域为单个数据库。 因此，在一个数据库中定义的 UDT 不能用在另一个数据库的列定义中。 要在多个数据库中使用 UDT，必须对各个数据库中的相同程序集执行 CREATE ASSEMBLY 和 CREATE TYPE 语句。 如果各个程序集具有相同的名称、强名称、区域性、版本、权限集和二进制内容，即可将它们视为相同。  
  
 一旦在两个数据库中注册了 UDT 并且均可从中访问它，即可将一个数据库的 UDT 值进行转换，用于另一个数据库。 可以在以下情况下跨数据库使用相同的 UDT：  
  
-   调用不同数据库中定义的存储过程。  
  
-   查询不同数据库中定义的表。  
  
-   选择一个数据库表 UDT 列中的 UDT 数据，然后将其插入另一个具有相同 UDT 列的数据库。  
  
 在上述情况下，自动执行服务器所需的任何转换。 您无法使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 或 CONVERT 函数显式执行转换。  
  
 请注意，在[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]**tempdb**系统数据库中创建工作台时，不需要执行任何使用 UDT 的操作。 这包括处理游标、表变量和用户定义的表值函数，这些函数包括 UDT 并透明地使用**tempdb**。 但是，如果在**tempdb**中显式创建定义 UDT 列的临时表，则必须以与用户数据库相同的方式在**tempdb**中注册 UDT。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
