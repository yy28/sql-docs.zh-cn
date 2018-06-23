---
title: 使用格式化文件跳过数据字段 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a60d4d668cb9c7d7d13a60a12df1057b24eea465
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125865"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>使用格式化文件跳过数据字段 (SQL Server)
  数据文件所包含的字段数可能大于表中的列数。 本主题说明了通过修改非 XML 和 XML 格式化文件，将表中的列映射到相应的数据字段并忽略额外字段，从而能够使用具有较多字段的数据文件。  
  
> [!NOTE]  
>  可以使用非 XML 或 XML 格式化文件将数据文件批量导入表中，方法是使用 **bcp** 命令、BULK INSERT 语句或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 语句。 有关详细信息，请参阅[使用格式化文件批量导入数据 (SQL Server)](use-a-format-file-to-bulk-import-data-sql-server.md)。  
  
## <a name="sample-data-file-and-table"></a>示例数据文件和表  
 本主题中修改的格式化文件示例基于下面的表和数据文件。  
  
### <a name="sample-table"></a>示例表  
 这些示例要求在 `myTestSkipField` 示例数据库中的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 架构下创建名为 `dbo` 的表。 若要创建此表，请在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器中运行以下代码：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipField   
   (  
   PersonID smallint,  
   FirstName nvarchar(50) ,  
   LastName nvarchar(50)   
   );  
GO  
```  
  
### <a name="sample-data-file"></a>示例数据文件  
 数据文件 `myTestSkipField-c.dat`包含下列记录：  
  
```  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
```  
  
 若要将数据从 `myTestSkipField-c.dat` 大容量导入至 `myTestSkipField` 表，则该格式化文件必须进行下列操作：  
  
-   将第一个数据字段映射到第一列 `PersonID`。  
  
-   跳过第二个数据字段。  
  
-   将第三个数据字段映射到第二列 `FirstName`。  
  
-   将第四个数据字段映射到第三列 `LastName`。  
  
## <a name="non-xml-format-file-for-more-data-fields"></a>针对较多数据字段的非 XML 格式化文件  
 以下格式化文件 `myTestSkipField.fmt` 将 `myTestSkipField-c.dat` 中的字段映射至 `myTestSkipField` 表的列。 该格式化文件使用字符数据格式。 跳过列映射需要将列顺序值更改为 0，如格式化文件中 `ExtraField` 列所示。  
  
 `myTestSkipField.fmt` 格式化文件包含以下信息：  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     PersonID               ""  
2       SQLCHAR       0       100       ","    0     ExtraField             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   3     LastName               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  有关非 XML 格式化文件语法的信息，请参阅[非 XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)。  
  
### <a name="examples"></a>示例  
 以下示例所用的 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 中使用了 `myTestSkipField.fmt` 格式化文件。 此示例将 `myTestSkipField-c.dat` 数据文件大容量导入至 `myTestSkipField` 表。 若要创建示例表和数据文件，请参阅本主题前面的“示例数据文件和表”。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器中，运行以下代码：  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
   SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.fmt'    
       ) AS t1;  
GO   
```  
  
## <a name="xml-format-file-for-more-data-fields"></a>针对较多数据字段的 XML 格式化文件  
 在示例中显示的格式化文件基于另一格式化文件 `myTestSkipField.xml`，该格式化文件始终使用字符数据格式并且其字段与 `myTestSkipField` 表中列的数量和顺序完全一致。 若要查看该格式化文件的内容，请参阅[创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)。  
  
 以下格式化文件 `myTestSkipField.xml` 将 `myTestSkipField-c.dat` 中的字段映射至 `myTestSkipField` 表的列。 该格式化文件使用字符数据格式。  
  
 `myTestSkipField.xml` 格式化文件包含以下信息：  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
### <a name="examples"></a>示例  
 以下示例所用的 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 中使用了 `myTestSkipField.Xml` 格式化文件。 此示例将 `myTestSkipField-c.dat` 数据文件大容量导入至 `myTestSkipField` 表。 若要创建示例表和数据文件，请参阅本主题前面的“示例数据文件和表”。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器中，运行以下代码：  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
  SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.xml'    
       ) AS t1;  
GO  
  
```  
  
> [!NOTE]  
>  有关 XML 架构语法和 XML 格式化文件的其他示例的信息，请参阅 [XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [使用格式化文件跳过表列 (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [使用格式化文件将表列映射到数据文件字段 (SQL Server)](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
