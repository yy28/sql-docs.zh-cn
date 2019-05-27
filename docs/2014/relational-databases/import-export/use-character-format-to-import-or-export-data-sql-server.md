---
title: 使用字符格式导入或导出数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab658be26dc8ccbdd4e760d0b1bc835ace3b2c38
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011670"
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>使用字符格式导入或导出数据 (SQL Server)
  将数据批量导出到要在其他程序中使用的文本文件时，或从其他程序生成的文本文件批量导入数据时，建议使用字符格式。  
  
> [!NOTE]  
>  当你在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例之间批量传输数据，且数据文件包含 Unicode 字符数据，但不包含任何扩展字符或 DBCS 字符时，请使用 Unicode 字符格式。 有关详细信息，请参阅 [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)。  
  
 采用字符格式后，所有列均应用字符数据格式。 如果要将数据用于其他程序（如电子表格程序），或需要通过其他数据库供应商（如 Oracle）将数据复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中，则以字符格式存储信息会非常有用。  
  
## <a name="considerations-for-using-character-format"></a>使用字符格式的注意事项  
 使用字符格式时，请考虑下列事项：  
  
-   默认情况下，**bcp** 实用工具使用制表符分隔字符数据字段，并用换行符终止记录。 有关如何指定替换终止符的详细信息，请参阅[指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)。  
  
-   默认情况下，在批量导出或导入字符模式数据之前，将执行下列转换：  
  
    |批量操作的方向|转换|  
    |---------------------------------|----------------|  
    |导出|将数据转换为字符表示形式。 如果进行显式请求，字符列的数据将转换为所请求的代码页。 如果未指定代码页，将通过使用客户端计算机的 OEM 代码页对字符数据进行转换。|  
    |导入|必要时将字符数据转换为本机表示形式，并将字符数据从客户端的代码页转换到目标列的代码页。|  
  
-   为避免在转换期间丢失扩展字符，请使用 Unicode 字符格式或指定代码页。  
  
-   存储在字符格式文件中的所有 `sql_variant` 数据都是在不包括元数据的情况下进行存储的。 每个数据值都将按照隐式数据转换规则转换为 `char` 格式。 当数据导入到 `sql_variant` 列中时，该数据是以 `char` 格式导入的。 而导入到数据类型不是 `sql_variant` 的列中时，数据将通过隐式转换从 `char` 格式转换为其他格式。 有关数据转换的详细信息，请参阅[数据类型转换（数据库引擎）](/sql/t-sql/data-types/data-type-conversion-database-engine)。  
  
-   **Bcp**实用工具导出`money`值作为字符格式数据文件与四位数字的小数点后且不包含诸如逗号分隔符之类的任何数字分组符号。 例如，包含值 1,234,567.123456 的 `money` 列将以字符串 1234567.1235 的形式大容量导出到数据文件中。  
  
## <a name="command-options-for-character-format"></a>字符格式的命令选项  
 你可以使用 **bcp**、BULK INSERT 或 INSERT ...选择\*从 OPENROWSET （BULK）。对于 **bcp** 命令或 BULK INSERT 语句，你可以在命令行中指定数据格式。 对于 INSERT ... SELECT * FROM OPENROWSET(BULK...) 语句，您必须在格式化文件中指定数据格式。  
  
 下列命令行选项支持字符格式：  
  
|Command|Option|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-c**|将导致**bcp**实用工具使用字符数据。<sup>1</sup>|  
|BULK INSERT|DATAFILETYPE **='char'**|在批量导入数据时使用字符格式。|  
  
 <sup>1</sup>加载字符 (**-c**) 到与早期版本的兼容的格式数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端，使用 **-V**切换。 有关详细信息，请参阅 [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)。  
  
 有关详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md)、[BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式化文件中为每个字段指定格式设置。 有关详细信息，请参阅 [用来导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
## <a name="examples"></a>示例  
 下面的示例介绍了如何使用 **bcp** 批量导出字符数据，以及如何使用 BULK INSERT 批量导入相同的数据。  
  
### <a name="sample-table"></a>示例表  
 这些示例要求 **dbo** 架构下的 **AdventureWorks** 示例数据库中存在名为 **myTestCharData** 的表。 必须先创建此表，才能运行这些示例。 若要创建此表，请在 SQL [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中执行以下内容：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要填充此表并查看得到的内容，请执行以下语句：  
  
```  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData  
  
```  
  
### <a name="using-bcp-to-bulk-export-character-data"></a>使用 bcp 大容量导出字符数据  
 若要将表中数据导出到数据文件，请将 **bcp** 与 **out** 选项和以下限定符结合使用：  
  
|限定符|Description|  
|----------------|-----------------|  
|**-c**|指定字符格式。|  
|**-t** `,`|将逗号 (`,`) 指定为字段终止符。<br /><br /> 注意：默认字段终止符是制表符 (\t)。 有关详细信息，请参阅 [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)。|  
|**-T**|指定 **bcp** 实用工具通过使用集成安全性的受信任连接连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，则需要指定 **-U** 和 **-P** 才能成功登录。|  
  
 下面的示例将 `myTestCharData` 表中的字符格式数据大容量导出到使用逗号 (,) 作为字段终止符且名为 `myTestCharData-c.Dat` 的新数据文件。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks..myTestCharData out C:\myTestCharData-c.Dat -c -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-character-data"></a>使用 BULK INSERT 大容量导入字符数据  
 以下示例使用 BULK INSERT 将 `myTestCharData-c.Dat` 数据文件中的数据导入到 `myTestCharData` 表中。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestCharData   
   FROM 'C:\myTestCharData-c.Dat'   
   WITH (  
      DATAFILETYPE='char',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
