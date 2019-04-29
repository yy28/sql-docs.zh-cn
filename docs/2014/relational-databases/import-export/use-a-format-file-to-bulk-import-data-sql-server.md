---
title: 使用格式化文件批量导入数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fddec2033997a1b76f34fa9a2fe006d385bc0132
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155857"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>使用格式化文件大容量导入数据 (SQL Server)
  本主题说明如何在大容量导入操作中使用格式化文件。 格式化文件将数据文件的各字段映射到表的各列。  当使用 **bcp** 命令、BULK INSERT 或 INSERT ...SELECT * FROM OPENROWSET(BULK...) [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令时，可以使用非 XML 或 XML 格式化文件大容量导入数据。  
  
> [!IMPORTANT]  
>  对于用于 Unicode 字符数据文件的格式化文件，所有输入字段必须为 Unicode 文本字符串（即固定大小 Unicode 字符串或字符终止 Unicode 字符串）。  
  
> [!NOTE]  
>  如果您不了解格式化文件，请参阅[非 XML 格式化文件&#40;SQL Server&#41; ](xml-format-files-sql-server.md)并[XML 格式化文件&#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
## <a name="format-file-options-for-bulk-import-commands"></a>大容量导入命令的格式化文件选项  
 下表汇总了各个大容量导入命令的格式化文件选项。  
  
|大容量加载命令|使用格式化文件选项|  
|------------------------|-----------------------------------|  
|BULK INSERT|FORMATFILE = '*format_file_path*'|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|FORMATFILE = '*format_file_path*'|  
|**bcp** ... **in**|**-f** *format_file*|  
  
 有关详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md)、[BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  若要大容量导出或导入 SQLXML 数据，请在格式化文件中使用下列数据类型之一：SQLCHAR 或 SQLVARYCHAR（数据以客户端代码页或排序规则隐含的代码页的形式发送）、SQLNCHAR 或 SQLNVARCHAR（数据以 Unicode 的形式发送）或者 SQLBINARY 或 SQLVARYBIN（数据不经任何转换直接发送）。  
  
## <a name="examples"></a>示例  
 本节中的示例说明了如何通过 **bcp** 命令和 BULK INSERT、INSERT ...SELECT * FROM OPENROWSET(BULK...) 语句使用格式化文件大容量导入数据。 运行这些大容量导入示例之前，都必须先创建示例表、数据文件和格式化文件。  
  
### <a name="sample-table"></a>示例表  
 这些示例要求在 **示例数据库中的** dbo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 架构下创建名为 **myTestFormatFiles** 的表。 若要创建此表，请在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中执行以下语句：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestFormatFiles (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50),  
   Col4 nvarchar(50)  
   );  
GO  
```  
  
### <a name="sample-data-file"></a>示例数据文件  
 这些示例使用包含以下记录的示例数据文件 `myTestFormatFiles-c.Dat`。 若要创建数据文件，请在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入以下内容：  
  
```  
10,Field2,Field3,Field4  
15,Field2,Field3,Field4  
46,Field2,Field3,Field4  
58,Field2,Field3,Field4  
```  
  
### <a name="sample-format-files"></a>示例格式化文件  
 本节中的一些示例使用的是 XML 格式化文件 `myTestFormatFiles-f-x-c.Xml`，而另一些示例使用的是非 XML 格式化文件。 这两种格式化文件都使用字符数据格式和非默认字段终止符 (,)。  
  
#### <a name="the-sample-non-xml-format-file"></a>示例非 XML 格式化文件  
 下面的示例使用 **bcp** 基于 `myTestFormatFiles` 表生成一个 XML 格式化文件。 `myTestFormatFiles.Fmt` 文件包含以下信息：  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     ","      2     Col2         SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      3     Col3         SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   4     Col4         SQL_Latin1_General_CP1_CI_AS  
```  
  
 若要使用带 **format** 选项的 **bcp** 创建此格式化文件，请在 Windows 命令提示符下输入以下内容：  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -f myTestFormatFiles.Fmt -T  
  
```  
  
 有关创建格式化文件的详细信息，请参阅[创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)。  
  
#### <a name="the-sample-xml-format-file"></a>示例 XML 格式化文件  
 下面的示例使用 **bcp** 进行创建，以基于 `myTestFormatFiles` 表生成一个 XML 格式化文件。 `myTestFormatFiles.Xml` 文件包含以下信息：  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 若要使用带 **format** 选项的 **bcp** 创建此格式化文件，请在 Windows 命令提示符下输入以下内容：  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -x -f myTestFormatFiles.Xml -T  
```  
  
### <a name="using-bcp"></a>使用 bcp  
 下面的示例使用 **bcp** 将数据从 `myTestFormatFiles-c.Dat` 数据文件批量导入到示例数据库的 `HumanResources.myTestFormatFiles` 表中。 此示例使用一个名为 `MyTestFormatFiles.Xml`的 XML 格式化文件。 此示例在导入数据文件之前删除所有的现有表行。  
  
 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp AdventureWorks2012..myTestFormatFiles in C:\myTestFormatFiles-c.Dat -f C:\myTestFormatFiles.Xml -T  
```  
  
> [!NOTE]  
>  有关此命令的详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md)。  
  
### <a name="using-bulk-insert"></a>使用 BULK INSERT  
 下面的示例使用 BULK INSERT 将数据从 `myTestFormatFiles-c.Dat` 数据文件大容量导入到 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 示例数据库中的 `HumanResources.myTestFormatFiles` 表中。 此示例使用的是非 XML 格式化文件 `MyTestFormatFiles.Fmt`。 此示例在导入数据文件之前删除所有的现有表行。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks2012;  
GO  
DELETE myTestFormatFiles;  
GO  
BULK INSERT myTestFormatFiles   
   FROM 'C:\myTestFormatFiles-c.Dat'   
   WITH (FORMATFILE = 'C:\myTestFormatFiles.Fmt');  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
> [!NOTE]  
>  有关此语句的详细信息，请参阅 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
### <a name="using-the-openrowset-bulk-rowset-provider"></a>使用 OPENROWSET 大容量行集提供程序  
 下面的示例使用 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 将数据从 `myTestFormatFiles-c.Dat` 数据文件大容量导入到 `HumanResources.myTestFormatFiles` 示例数据库的 `AdventureWorks` 表中。 此示例使用一个名为 `MyTestFormatFiles.Xml`的 XML 格式化文件。 此示例在导入数据文件之前删除所有的现有表行。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks2012;  
DELETE myTestFormatFiles;  
GO  
INSERT INTO myTestFormatFiles  
    SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestFormatFiles-c.Dat',  
      FORMATFILE='C:\myTestFormatFiles.Xml'       
      ) as t1 ;  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
 用完示例表后，可以使用以下语句删除该表：  
  
```  
DROP TABLE myTestFormatFiles  
```  
  
> [!NOTE]  
>  有关 OPENROWSET BULK 子句的详细信息，请参阅 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
## <a name="additional-examples"></a>其他示例  
 [创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)  
  
 [使用格式化文件跳过表列 (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 [使用格式化文件跳过数据字段 (SQL Server)](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
 [使用格式化文件将表列映射到数据文件字段 (SQL Server)](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [非 XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)   
 [XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)  
  
  
