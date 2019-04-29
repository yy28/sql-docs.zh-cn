---
title: 在批量导入期间保留 Null 或使用默认值 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4753e1097dee300d4d806c42b71954e6e557ed12
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063924"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>在批量导入期间保留 Null 或使用默认值 (SQL Server)
  默认情况下，将数据导入表中时， **bcp** 命令和 BULK INSERT 语句将使用为表中的列定义的默认值。 例如，如果数据文件中包含一个空字段，则会加载该列的默认值。 **bcp** 命令和 BULK INSERT 语句都允许指定保留空值。  
  
 相反，常规 INSERT 语句会保留空值而不会插入默认值。 INSERT ... SELECT * FROM OPENROWSET(BULK...) 语句的基本行为与常规 INSERT 相同，但前者还支持插入默认值的表提示。  
  
> [!NOTE]  
>  有关跳过某个表列的格式化文件示例，请参阅[使用格式化文件跳过表列 (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)。  
  
## <a name="sample-table-and-data-file"></a>示例表和数据文件  
 若要运行本主题中的示例，需要创建示例表和数据文件。  
  
### <a name="sample-table"></a>示例表  
 这些示例要求 **dbo** 架构下的 **AdventureWorks** 示例数据库中存在名为 **MyTestDefaultCol2** 的表。 若要创建此表，请在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器中执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE MyTestDefaultCol2   
(Col1 smallint,  
Col2 nvarchar(50) DEFAULT 'Default value of Col2',  
Col3 nvarchar(50)   
);  
GO  
  
```  
  
 注意，第二个表列 ( `Col2`) 具有默认值。  
  
### <a name="sample-format-file"></a>示例格式化文件  
 某些大容量导入示例使用非 XML 格式化文件 `MyTestDefaultCol2-f-c.Fmt`，它与 `MyTestDefaultCol2` 表完全一致。 若要创建此格式化文件，请在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 format nul -c -f C:\MyTestDefaultCol2-f-c.Fmt -t, -r\n -T  
  
```  
  
 有关创建格式化文件的详细信息，请参阅[创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)。  
  
### <a name="sample-data-file"></a>示例数据文件  
 该示例使用示例数据文件 `MyTestEmptyField2-c.Dat`，它的第二个字段中不包含值。 `MyTestEmptyField2-c.Dat` 数据文件包含下列记录。  
  
```  
1,,DataField3  
2,,DataField3  
  
```  
  
## <a name="keeping-null-values-with-bcp-or-bulk-insert"></a>使 bcp 或 BULK INSERT 保留空值  
 下列限定符指定在大容量导入操作期间数据文件中的空字段保留其空值，而不继承表列的默认值（如果存在）。  
  
|Command|Qualifier|限定符类型|  
|-------------|---------------|--------------------|  
|**bcp**|`-k`|开关|  
|BULK INSERT|KEEPNULLS<sup>1</sup>|参数|  
  
 <sup>1</sup>对于 BULK INSERT，如果默认值不可用，必须将表列定义为允许 null 值。  
  
> [!NOTE]  
>  这些限定符通过这些大容量导入命令禁止检查表上的 DEFAULT 定义。 然而，对于任何并发 INSERT 语句，都需要 DEFAULT 定义。  
  
 有关详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md) 和 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
### <a name="examples"></a>示例  
 本节中的示例使用 **bcp** 或 BULK INSERT 进行批量导入并保留 null 值。  
  
 第二个表列 **Col2**具有默认值。 数据文件的相应字段包含空字符串。 默认情况下，当 **bcp** 或 BULK INSERT 用于将数据从此数据文件导入 **MyTestDefaultCol2** 表时，将插入 **Col2** 的默认值，这会产生下列结果：  
  
||||  
|-|-|-|  
|`1`|`Default value of Col2`|`DataField3`|  
|`2`|`Default value of Col2`|`DataField3`|  
  
 要插入"`NULL`"而不是 of"`Default value of Col2`"，您需要使用`-k`开关或 KEEPNULL 选项，如以下所示**bcp**和 BULK INSERT 示例。  
  
#### <a name="using-bcp-and-keeping-null-values"></a>使用 bcp 并保留空值  
 下列示例演示如何在 **bcp** 命令中保留 null 值。 **bcp** 命令包含以下开关：  
  
|开关|Description|  
|------------|-----------------|  
|`-f`|指定命令使用格式化文件。|  
|`-k`|指定在操作过程中空列应该保留 null 值，而不是所插入列的任何默认值。|  
|`-T`|指定 bcp 实用工具使用可信连接来连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
  
 在 Windows 命令提示符下输入。  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 in C:\MyTestEmptyField2-c.Dat -f C:\MyTestDefaultCol2-f-c.Fmt -k -T  
  
```  
  
#### <a name="using-bulk-insert-and-keeping-null-values"></a>使用 BULK INSERT 并保留空值  
 下面的示例演示如何使用 BULK INSERT 语句中的 KEEPNULLS 选项。 在查询工具（如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器）中执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT MyTestDefaultCol2  
   FROM 'C:\MyTestEmptyField2-c.Dat'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      KEEPNULLS  
   );  
GO  
  
```  
  
## <a name="keeping-default-values-with-insert--select--from-openrowsetbulk"></a>使用 INSERT ... SELECT * FROM OPENROWSET(BULK...)  
 默认情况下，未在大容量加载操作中指定的所有列都被 INSERT ... SELECT * FROM OPENROWSET(BULK...) 将本机格式数据导入到表中。但是，对于数据文件中的空字段，您可以指定相应的表列使用其默认值（如果存在）。 若要使用默认值，请指定下列表提示：  
  
|Command|Qualifier|限定符类型|  
|-------------|---------------|--------------------|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|WITH(KEEPDEFAULTS)|表提示|  
  
> [!NOTE]  
>  有关详细信息，请参阅 [INSERT (Transact-SQL)](/sql/t-sql/statements/insert-transact-sql)、[SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)、[OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql) 和[表提示 (SQL Server)](/sql/t-sql/queries/hints-transact-sql-table)  
  
### <a name="examples"></a>示例  
 下列 INSERT ... SELECT * FROM OPENROWSET(BULK...) 示例将大容量导入数据并保留默认值。  
  
 若要运行这些示例，需要创建 **MyTestDefaultCol2** 示例表和 `MyTestEmptyField2-c.Dat` 数据文件，并使用格式化文件 `MyTestDefaultCol2-f-c.Fmt`。 有关创建这些示例的信息，请参阅本主题前面的“示例表和数据文件”。  
  
 第二个表列 **Col2**具有默认值。 数据文件的相应字段包含空字符串。 当 INSERT ... SELECT \* FROM OPENROWSET(BULK...) 将该数据文件中的字段导入 **MyTestDefaultCol2** 表时，默认情况下，NULL（而不是默认值）将被插入到 **Col2** 中。 此默认的行为产生下列结果：  
  
||||  
|-|-|-|  
|`1`|`NULL`|`DataField3`|  
|`2`|`NULL`|`DataField3`|  
  
 若要插入默认值“`Default value of Col2`”代替“`NULL`”，需要使用 KEEPDEFAULTS 表提示，如下面的示例所示。 在查询工具（如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器）中执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
INSERT INTO MyTestDefaultCol2  
    WITH (KEEPDEFAULTS)  
    SELECT *  
      FROM OPENROWSET(BULK  'C:\MyTestEmptyField2-c.Dat',  
      FORMATFILE='C:\MyTestDefaultCol2-f-c.Fmt'       
      ) as t1 ;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [批量导入数据时保留标识值 (SQL Server)](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [准备用于批量导出或导入的数据 (SQL Server)](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **使用格式化文件**  
  
-   [创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式化文件将表列映射到数据文件字段 (SQL Server)](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [使用格式化文件跳过数据字段 (SQL Server)](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式化文件跳过表列 (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **在使用 bcp 时指定数据格式以获得兼容性**  
  
-   [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)  
  
-   [使用 bcp 指定数据文件中的前缀长度 (SQL Server)](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [使用 bcp 指定文件存储类型 (SQL Server)](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [表提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
