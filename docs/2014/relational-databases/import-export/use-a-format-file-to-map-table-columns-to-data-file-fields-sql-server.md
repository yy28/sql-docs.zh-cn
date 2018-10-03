---
title: 使用格式化文件将表列映射到数据文件字段 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a35a70da1dac3d6dd2ff5e37f696654960883810
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229017"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>使用格式化文件将表列映射到数据文件字段 (SQL Server)
  数据文件中包含的字段的排列顺序可能不同于表中相应列的顺序。 本主题介绍了非 XML 格式化文件和 XML 格式化文件，它们经过修改可容纳字段排列顺序不同于表列顺序的数据文件。 修改后的格式化文件可将数据字段映射到与之相应的表列。  
  
> [!NOTE]  
>  非 XML 格式化文件或 XML 格式化文件都可以用来将数据文件大容量导入表中，方法是使用 **bcp** 命令、BULK INSERT 语句或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 语句。 有关详细信息，请参阅[使用格式化文件批量导入数据 (SQL Server)](use-a-format-file-to-bulk-import-data-sql-server.md)。  
  
## <a name="sample-table-and-data-file"></a>示例表和数据文件  
 本主题中修改的格式化文件示例基于下面的表和数据文件。  
  
### <a name="sample-table"></a>示例表  
 本主题中的示例要求在 `myTestOrder` 示例数据库中的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 架构下创建名为 `dbo` 的表。 若要创建此表，请在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器中执行以下代码：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestOrder   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) ,  
   Col3 nvarchar(50) ,   
   Col4 nvarchar(50)   
   );  
GO  
  
```  
  
### <a name="data-file"></a>数据文件  
 数据文件 `myTestOrder-c.txt`包含下列记录：  
  
```  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
  
```  
  
 若要将数据从 `myTestSkipCol2-c.dat` 大容量导入 `myTestSkipCol` 表中，格式化文件必须将第一个数据字段映射到 `Col3`、将第二个数据字段映射到 `Col2`、将第三个数据字段映射到 `Col1`、将第四个数据字段映射到 `Col4`。  
  
## <a name="using-a-non-xml-format-file"></a>使用非 XML 格式化文件  
 可通过更改列的顺序值来更改列映射的顺序，以指示相应数据字段的位置。  
  
 下面的非 XML 格式化文件示例提供了一个格式化文件 `myTestOrder.fmt`，它将 `myTestOrder-c.txt` 中的字段映射到 `myTestOrder` 表中的列。 有关如何创建数据文件和表的信息，请参阅本主题前面的“示例表和数据文件”部分。 该格式化文件使用字符数据格式。  
  
 格式化文件中包含下列信息：  
  
```  
9.0  
4  
1       SQLCHAR       0       100     ","     3     Col3               SQL_Latin1_General_CP1_CI_AS  
2       SQLCHAR       0       100     ","     2     Col2               SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       7       ","     1     Col1               ""  
4       SQLCHAR       0       100     "\r\n"  4     Col4               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  有关非 XML 格式文件布局的详细信息，请参阅[非 XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)。  
  
### <a name="example"></a>示例  
 下面的示例使用非 XML 格式化文件 `BULK INSERT`，通过 `myTestOrder-c.txt` 语句将数据文件 `myTestOrder` 中的数据大容量导入示例表 `myTestOrder.fmt` 中。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行：  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestOrder  
FROM 'C:\myTestOrder-c.txt'   
WITH (formatfile='C:\myTestOrder.fmt');  
GO  
  
```  
  
## <a name="using-an-xml-format-file"></a>使用 XML 格式化文件  
 下面的非 XML 格式化文件示例提供了一个格式化文件 `myTestOrder.xml`，它将 `myTestOrder-c.txt` 中的字段映射到 `myTestOrder` 表中的列。有关如何创建数据文件和表的信息，请参阅本主题前面的“示例表和数据文件”部分。  
  
 `myTestOrder.xml` 格式化文件包含以下信息：  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="3" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="1" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
  
```  
  
> [!NOTE]  
>  有关 XML 架构语法和 XML 格式化文件的其他示例的信息，请参阅 [XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)。  
  
### <a name="example"></a>示例  
 下面的示例使用 XML 格式化文件 `OPENROWSET` ，通过 `myTestOrder-c.txt` 大容量行集提供程序将数据文件 `myTestOrder` 中的数据导入示例表 `myTestOrder.xml` 中。 `INSERT… SELECT` 语句指定选择列表中的列。  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行下列代码：  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestOrder   
  SELECT Col1, Col2, Col3, Col4  
      FROM  OPENROWSET(BULK  'C:\myTestOrder-c.txt',  
      FORMATFILE='C:\myTestOrder.Xml'    
       ) AS t1;  
GO  
  
```  
  
## <a name="see-also"></a>请参阅  
 [使用格式化文件跳过表列 (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [使用格式化文件跳过数据字段 (SQL Server)](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  
