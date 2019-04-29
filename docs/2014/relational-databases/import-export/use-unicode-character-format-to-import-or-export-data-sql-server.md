---
title: 使用 Unicode 字符格式导入或导出数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 85df40b07542e1af144796d4e8b5f9fb33cdc7c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065750"
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>使用 Unicode 字符格式导入或导出数据 (SQL Server)
  使用包含扩展/DBCS 字符的数据文件在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间大容量传输数据时，建议使用 Unicode 字符格式。 从服务器导出数据时，Unicode 字符数据格式允许使用与执行该操作的客户端不同的代码页。 在这种情况下，使用 Unicode 字符格式有下列优点：  
  
-   如果源数据和目标数据的类型为 Unicode，则使用 Unicode 字符格式可以保留所有的字符数据。  
  
-   如果源数据和目标数据的类型不为 Unicode，则使用 Unicode 字符格式可以尽可能减少丢失源数据中无法在目标数据中表示的扩展字符。  
  
 Unicode 字符格式数据文件遵循 Unicode 文件的约定。 该文件的前两个字节为十六进制数字 0xFFFE。 这两个字节用作字节顺序标记，指定在文件中高位字节是存储在前面还是后面。  
  
> [!IMPORTANT]  
>  对于用于 Unicode 字符数据文件的格式化文件，所有输入字段必须为 Unicode 文本字符串（即固定大小 Unicode 字符串或字符终止 Unicode 字符串）。  
  
 Unicode 字符格式数据文件中存储的 `sql_variant` 数据的操作方式与字符格式数据文件中的同类数据的操作方式相同，唯一的不同是该数据存储为 `nchar` 而不是 `char` 数据。 有关字符格式的详细信息，请参阅 [Collation and Unicode Support](../collations/collation-and-unicode-support.md)。  
  
 若要使用与 Unicode 字符格式提供的默认终止符不同的字段终止符或行终止符，请参阅[指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)。  
  
## <a name="command-options-for-unicode-character-format"></a>Unicode 字符格式的命令选项  
 你可以使用 **bcp**、BULK INSERT 或 INSERT ...选择\*从 OPENROWSET （BULK）。对于 **bcp** 命令或 BULK INSERT 语句，你可以在命令行中指定数据格式。 对于 INSERT ... SELECT * FROM OPENROWSET(BULK...) 语句，您必须在格式化文件中指定数据格式。  
  
 下列命令行选项支持 Unicode 字符格式：  
  
|Command|Option|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-w**|使用 Unicode 字符格式。|  
|BULK INSERT|DATAFILETYPE **='** widechar **'**|批量导入数据时使用 Unicode 字符格式。|  
  
 有关详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md)、[BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式化文件中为每个字段指定格式设置。 有关详细信息，请参阅 [用来导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
## <a name="examples"></a>示例  
 下面的示例展示了如何使用 **bcp** 批量导出 Unicode 字符数据，以及如何使用 BULK INSERT 批量导入相同的数据。  
  
### <a name="sample-table"></a>示例表  
 这些示例要求在 `myTestUniCharData` 示例数据库中的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 架构下创建名为 `dbo` 的表。 必须先创建此表，才能运行这些示例。 若要创建此表，请在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中执行以下语句：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestUniCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要填充此表并查看得到的内容，请执行以下语句：  
  
```  
INSERT INTO myTestUniCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3')   
        ,(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
  
```  
  
### <a name="using-bcp-to-bulk-export-unicode-character-data"></a>使用 bcp 大容量导出 Unicode 字符数据  
 若要将表中数据导出到数据文件，请将 **bcp** 与 **out** 选项和以下限定符结合使用：  
  
|限定符|Description|  
|----------------|-----------------|  
|**-w**|指定 Unicode 字符格式。|  
|**-t** `,`|将逗号 (`,`) 指定为字段终止符。<br /><br /> 注意：默认字段终止符是 Unicode 制表符 (\t)。 有关详细信息，请参阅 [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)。|  
|**-T**|指定 **bcp** 实用工具通过使用集成安全性的受信任连接连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T**，则需要指定 **-U** 和 **-P** 才能成功登录。|  
  
 以下示例将 Unicode 字符格式的数据从 `myTestUniCharData` 表中大容量导出到名为 `myTestUniCharData-w.Dat` 的新数据文件，此数据文件使用逗号 (`,`) 作为字段终止符。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks2012..myTestUniCharData out C:\myTestUniCharData-w.Dat -w -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-unicode-character-data"></a>使用 BULK INSERT 大容量导入 Unicode 字符数据  
 以下示例使用 `BULK INSERT` 将 `myTestUniCharData-w.Dat` 数据文件中的数据导入 `myTestUniCharData` 表。 必须在语句中声明非默认字段终止符 (`,`)。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestUniCharData   
   FROM 'C:\myTestUniCharData-w.Dat'   
   WITH (  
      DATAFILETYPE='widechar',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [Collation and Unicode Support](../collations/collation-and-unicode-support.md)  
  
  
