---
title: 批量导入和导出 XML 文档的示例 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- field terminators [SQL Server]
- bulk importing [SQL Server], data formats
- row terminators [SQL Server]
- OPENROWSET function, XML bulk load
- terminators [SQL Server]
- bulk exporting [SQL Server], data formats
- XML bulk load [SQL Server]
ms.assetid: dff99404-a002-48ee-910e-f37f013d946d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d60518f64bd44b9b2498c9d27711d47753b04cf9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011968"
---
# <a name="examples-of-bulk-import-and-export-of-xml-documents-sql-server"></a>批量导入和导出 XML 文档的示例 (SQL Server)
    
##  <a name="top"></a>可以将 XML 文档大容量导入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到数据库中，也可以从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中大容量导出 XML 文档。 本主题提供了这两种情况的示例。  
  
 若要将数据从一个数据文件大容量导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表或未分区视图，可以使用以下工具或命令：  
  
-   **bcp** 实用工具  
  
     还可以使用 **bcp** 实用工具将数据从可执行 SELECT 语句的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的任意位置（包括分区视图）导出。  
  
-   BULK INSERT  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 有关详细信息，请参阅[使用 Bcp 实用工具导入和导出大容量数据 &#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)并[使用 BULK INSERT 或 OPENROWSET 导入大容量数据&#40;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)&#41; &#40;SQL Server&#41;。  
  
## <a name="examples"></a>示例  
 下列示例说明了以下操作内容：  
  
-   A. [以二进制字节流的形式大容量导入 XML 数据](#binary_byte_stream)  
  
-   B. [在现有行中大容量导入 XML 数据](#existing_row)  
  
-   C. [从包含 DTD 的文件中大容量导入 XML 数据](#file_contains_dtd)  
  
-   D. [使用格式化文件显式指定字段终止符](#field_terminator_in_format_file)  
  
-   E. [大容量导出 XML 数据](#bulk_export_xml_data)  
  
###  <a name="binary_byte_stream"></a>的. 以二进制字节流的形式大容量导入 XML 数据  
 在从文件大容量导入 XML 数据时，如果文件中包含要应用的编码声明，则应在 OPENROWSET(BULK…) 子句中指定 SINGLE_BLOB 选项。 SINGLE_BLOB 选项可确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XML 分析器根据 XML 声明中指定的编码方案导入数据。  
  
#### <a name="sample-table"></a>示例表  
 若要测试示例 A，必须创建示例表 `T`。  
  
```  
USE tempdb  
CREATE TABLE T (IntCol int, XmlCol xml);  
GO  
```  
  
#### <a name="sample-data-file"></a>示例数据文件  
 在运行示例 A 之前，必须先创建一个 UTF-8 编码文件 (`C:\SampleFolder\SampleData3.txt`)，该文件应包含指定 `UTF-8` 编码方案的以下示例实例。  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<Root>  
          <ProductDescription ProductModelID="5">  
             <Summary>Some Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-a"></a>示例 A  
 此示例使用 `SINGLE_BLOB` 语句中的 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 选项从名为 `SampleData3.txt` 的文件中导入数据，并在包含单列的示例表 `T`中插入一个 XML 实例。  
  
```  
INSERT INTO T(XmlCol)  
SELECT * FROM OPENROWSET(  
   BULK 'c:\SampleFolder\SampleData3.txt',  
   SINGLE_BLOB) AS x;  
```  
  
#### <a name="remarks"></a>备注  
 在这个例子中，通过使用 SINGLE_BLOB，可以避免 XML 文档的编码（由 XML 编码声明所指定）与服务器隐含使用的字符串代码页不匹配的问题。  
  
 如果使用 NCLOB 或 CLOB 数据类型且遇到代码页或编码冲突，则必须执行下列操作之一：  
  
-   删除 XML 声明，以成功导入 XML 数据文件的内容。  
  
-   在查询的 CODEPAGE 选项中指定一个代码页，该代码页须与 XML 声明中使用的编码方案相匹配。  
  
-   使用非 Unicode XML 编码方案匹配或解析数据库排序规则设置。  
  
 [&#91;Top&#93;](#top)  
  
###  <a name="existing_row"></a>B. 将 XML 数据大容量导入现有行中  
 此示例使用 `OPENROWSET` 大容量行集提供程序向示例表 `T`中的现有行添加一个 XML 实例。  
  
> [!NOTE]  
>  若要运行此示例，必须先完成示例 A 中提供的测试脚本。该示例创建了 `tempdb.dbo.T` 表，并从 `SampleData3.txt`中大容量导入数据。  
  
#### <a name="sample-data-file"></a>示例数据文件  
 示例 B 使用的是上例所使用 `SampleData3.txt` 示例数据文件的修改版本。 若要运行此示例，请按如下所示修改此文件的内容：  
  
```  
<Root>  
          <ProductDescription ProductModelID="10">  
             <Summary>Some New Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-b"></a>示例 B  
  
```  
-- Query before update shows initial state of XmlCol values.  
SELECT * FROM T  
UPDATE T  
SET XmlCol =(  
SELECT * FROM OPENROWSET(  
   BULK 'C:\SampleFolder\SampleData3.txt',  
           SINGLE_BLOB  
) AS x  
)  
WHERE IntCol = 1;  
GO  
```  
  
 [&#91;Top&#93;](#top)  
  
###  <a name="file_contains_dtd"></a>Ansi-c. 从包含 DTD 的文件中大容量导入 XML 数据  
  
> [!IMPORTANT]  
>  若非您的 XML 环境有特殊要求，建议不要启用对文档类型定义 (DTD) 的支持。 启用 DTD 支持会增加服务器的可攻击外围应用，并且可能会使它受到拒绝服务攻击。 如果必须启用 DTD 支持，可以通过仅处理可信的 XML 文档来降低安全风险。  
  
 在尝试使用 [bcp](../../tools/bcp-utility.md) 命令从包含 DTD 的文件中导入 XML 数据的过程中，可能会出现如下错误：  
  
 “SQLState = 42000，NativeError = 6359”  
  
 “错误 = [Microsoft][SQL Server Native Client][SQL Server]不允许使用内部子集 DTD 分析 XML。 请将 CONVERT 与样式选项 2 一起使用，以启用有限的内部子集 DTD 支持。”  
  
 “BCP 复制 %s 失败”  
  
 若要解决此问题，可以使用 `OPENROWSET(BULK...)` 函数，并在命令的 `CONVERT` 子句中指定 `SELECT` 选项，以从包含 DTD 的数据文件中导入 XML 数据。 该命令的基本语法如下：  
  
 `INSERT ... SELECT CONVERT(...) FROM OPENROWSET(BULK...)`  
  
#### <a name="sample-data-file"></a>示例数据文件  
 在测试此批量导入示例之前，需要先创建一个包含以下示例实例的文件 (`C:\temp\Dtdfile.xml`)：  
  
```  
<!DOCTYPE DOC [<!ATTLIST elem1 attr1 CDATA "defVal1">]><elem1>January</elem1>  
```  
  
#### <a name="sample-table"></a>示例表  
 示例 C 使用由以下 `T1` 语句创建的 `CREATE TABLE` 示例表：  
  
```  
USE tempdb;  
CREATE TABLE T1(XmlCol xml);  
GO  
```  
  
#### <a name="example-c"></a>示例 C  
 此示例使用 `OPENROWSET(BULK...)` ，并在 `CONVERT` 子句中指定了 `SELECT` 选项，从而将 XML 数据从 `Dtdfile.xml` 导入到了示例表 `T1`中。  
  
```  
INSERT T1  
  SELECT CONVERT(xml, BulkColumn, 2) FROM   
    OPENROWSET(Bulk 'c:\temp\Dtdfile.xml', SINGLE_BLOB) [rowsetresults];  
```  
  
 执行 `INSERT` 语句后，会将 DTD 从 XML 中提取出来，并存储到 `T1` 表中。  
  
 [&#91;Top&#93;](#top)  
  
###  <a name="field_terminator_in_format_file"></a>2-d. 使用格式化文件显式指定字段终止符  
 下面的示例说明如何大容量导入 XML 文档 `Xmltable.dat`。  
  
#### <a name="sample-data-file"></a>示例数据文件  
 
  `Xmltable.dat` 中的文档包含两个 XML 值，每行一个。 第一个 XML 值的编码为 UTF-16，第二个值的编码为 UTF-8。  
  
 下面的十六进制转储显示了此数据文件的内容：  
  
```  
FF FE 3C 00 3F 00 78 00-6D 00 6C 00 20 00 76 00  *..<.?.x.m.l. .v.*  
65 00 72 00 73 00 69 00-6F 00 6E 00 3D 00 22 00  *e.r.s.i.o.n.=.".*  
31 00 2E 00 30 00 22 00-20 00 65 00 6E 00 63 00  *1...0.". .e.n.c.*  
6F 00 64 00 69 00 6E 00-67 00 3D 00 22 00 75 00  *o.d.i.n.g.=.".u.*  
74 00 66 00 2D 00 31 00-36 00 22 00 3F 00 3E 00  *t.f.-.1.6.".?.>.*  
3C 00 72 00 6F 00 6F 00-74 00 3E 00 A2 4F 9C 76  *<.r.o.o.t.>..O.v*  
0C FA 77 E4 80 00 89 00-00 06 90 06 91 2E 9B 2E  *..w.............*  
99 34 A2 34 86 00 83 02-92 20 7F 02 4E C5 E4 A3  *.4.4..... ..N...*  
34 B2 B7 B3 B7 FE F8 FF-F8 00 3C 00 2F 00 72 00  *4.........<./.r.*  
6F 00 6F 00 74 00 3E 00-00 00 00 00 7A EF BB BF  *o.o.t.>.....z...*  
3C 3F 78 6D 6C 20 76 65-72 73 69 6F 6E 3D 22 31  *<?xml version="1*  
2E 30 22 20 65 6E 63 6F-64 69 6E 67 3D 22 75 74  *.0" encoding="ut*  
66 2D 38 22 3F 3E 3C 72-6F 6F 74 3E E4 BE A2 E7  *f-8"?><root>....*  
9A 9C EF A8 8C EE 91 B7-C2 80 C2 89 D8 80 DA 90  *................*  
E2 BA 91 E2 BA 9B E3 92-99 E3 92 A2 C2 86 CA 83  *................*  
E2 82 92 C9 BF EC 95 8E-EA 8F A4 EB 88 B4 EB 8E  *................*  
B7 EF BA B7 EF BF B8 C3-B8 3C 2F 72 6F 6F 74 3E  *.........</root>*  
00 00 00 00 7A                                   *....z*  
```  
  
#### <a name="sample-table"></a>示例表  
 大容量导入或导出 XML 文档时，应使用不可能出现在任何文档中的[字段终止符](specify-field-and-row-terminators-sql-server.md);例如，一系列四个 null （`\0`），后跟字母`z`：。 `\0\0\0\0z`  
  
 此示例说明如何为 `xTable` 示例表使用此字段终止符。 若要创建此示例表，请使用下列 `CREATE TABLE` 语句：  
  
```  
USE tempdb;  
CREATE TABLE xTable (xCol xml);  
GO  
```  
  
#### <a name="sample-format-file"></a>示例格式化文件  
 必须在格式化文件中指定字段终止符。 示例 D 使用了一个名为 `Xmltable.fmt` 的非 XML 格式化文件，该文件包含以下内容：  
  
```  
9.0  
1  
1       SQLBINARY     0       0       "\0\0\0\0z"    1     xCol         ""  
```  
  
 可以使用此格式化文件并通过 `xTable` 命令、 `bcp` 语句或 `BULK INSERT` 语句将 XML 文档大容量导入到 `INSERT ... SELECT * FROM OPENROWSET(BULK...)` 表中。  
  
#### <a name="example-d"></a>示例 D  
 此示例在 `Xmltable.fmt` 语句中使用 `BULK INSERT` 格式化文件来导入 XML 数据文件 `Xmltable.dat`中的内容。  
  
```  
BULK INSERT xTable   
FROM 'C:\Xmltable.dat'  
WITH (FORMATFILE = 'C:\Xmltable.fmt');  
GO  
```  
  
 [&#91;Top&#93;](#top)  
  
###  <a name="bulk_export_xml_data"></a>电邮. 大容量导出 XML 数据  
 下面的示例使用 `bcp` 命令和同一个 XML 格式化文件从上一示例所创建的表中大容量导出 XML 数据。 在下面的 `bcp` 命令中， `<server_name>` 和 `<instance_name>` 代表必须使用相应的值替换的占位符：  
  
```  
bcp bulktest..xTable out a-wn.out -N -T -S<server_name>\<instance_name>  
```  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保存 XML 编码。 因此，在导出 XML 数据时，XML 字段的原始编码将不可用。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导出 XML 数据时，使用 UTF-16 编码。  
  
 [&#91;Top&#93;](#top)  
  
## <a name="see-also"></a>另请参阅  
 [INSERT (Transact-SQL)](/sql/t-sql/statements/insert-transact-sql)   
 [SELECT 子句 &#40;Transact-sql&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [大容量导入和导出数据 &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
