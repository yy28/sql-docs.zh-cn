---
title: 使用 bcp 指定文件存储类型 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 307cc94aff7fb1e5f8f9bad99aac1c99c08fc293
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155824"
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>使用 bcp 指定文件存储类型 (SQL Server)
  “文件存储类型”  说明数据在数据文件中的存储方式。 数据可以按其数据库表类型（本机格式）、字符表示形式（字符格式）或支持隐式转换的任何数据类型导出到数据文件中；例如，以 `smallint` 形式复制 `int`。 用户定义的数据类型将按其基类型导出。  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>用于文件存储类型的 bcp 提示符  
 如果某个交互式 **bcp** 命令包含不带格式化文件开关 ( **-f** ) 或数据格式开关（ **-n** 、**-c**、**-w**或 **-N**）的 **in**或 **out**选项，则该命令会提示输入每个数据字段的文件存储类型，如下所示：  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 您对此提示符的响应取决于要执行的任务，如下所示：  
  
-   若要以尽可能大的压缩存储的格式（本机数据格式）将数据从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例批量导出到数据文件中，请接受 **bcp**提供的默认文件存储类型。 有关本机文件存储类型的列表，请参阅本主题后面所述的“本机文件存储类型”。  
  
-   若要以字符格式将数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例大容量导出到数据文件中，请指定 `char` 作为表中所有列的文件存储类型。  
  
-   若要将数据从数据文件大容量导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，对于以字符格式存储的类型，请将文件存储类型指定为 `char`，而对于以本机数据类型格式存储的数据，请按需指定以下文件存储类型之一：  
  
    |文件存储类型|在命令提示符下输入|  
    |-----------------------|-----------------------------|  
    |`char` <sup>1</sup>|`c`[`har`]|  
    |`varchar`|`c[har]`|  
    |`nchar`|`w`|  
    |`nvarchar`|`w`|  
    |`text` <sup>2</sup>|`T`[`ext`]|  
    |`ntext2`|`W`|  
    |`binary`|`x`|  
    |`varbinary`|`x`|  
    |`image` <sup>2</sup>|`I`[`mage`]|  
    |`datetime`|**d[ate]**|  
    |`smalldatetime`|`D`|  
    |`time`|`te`|  
    |`date`|`de`|  
    |`datetime2`|`d2`|  
    |`datetimeoffset`|`do`|  
    |`decimal`|`n`|  
    |`numeric`|`n`|  
    |`float`|**f[loat]**|  
    |`real`|`r`|  
    |`Int`|**i[nt]**|  
    |`bigint`|`B[igint]`|  
    |`smallint`|**s[mallint]**|  
    |`tinyint`|**t[inyint]**|  
    |`money`|**m[oney]**|  
    |`smallmoney`|`M`|  
    |`bit`|`b[it]`|  
    |`uniqueidentifier`|`u`|  
    |`sql_variant`|`V[ariant]`|  
    |`timestamp`|`x`|  
    |`UDT`（用户定义的数据类型）|`U`|  
    |`XML`|`X`|  
  
     <sup>1</sup>的字段长度、 前缀长度和终止符一起决定的非字符数据的导出为数据文件中分配的存储空间量`char`文件存储类型。  
  
     <sup>2</sup> `ntext`， `text`，和`image`中的未来版本将删除的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在新的开发工作中，请避免使用这些数据类型，并修改当前使用它们的应用程序。 相反，使用 `nvarchar(max)`、`varchar(max)` 和 `varbinary(max)`。  
  
## <a name="native-file-storage-types"></a>本机文件存储类型  
 在格式化文件中，每种本机文件存储类型都记录为相应的宿主文件数据类型。  
  
|文件存储类型|宿主文件数据类型|  
|-----------------------|-------------------------|  
|`char` <sup>1</sup>|SQLCHAR|  
|`varchar`|SQLCHAR|  
|`nchar`|SQLNCHAR|  
|`nvarchar`|SQLNCHAR|  
|`text` <sup>2</sup>|SQLCHAR|  
|`ntext` <sup>2</sup>|SQLNCHAR|  
|`binary`|SQLBINARY|  
|`varbinary`|SQLBINARY|  
|`image` <sup>2</sup>|SQLBINARY|  
|`datetime`|SQLDATETIME|  
|`smalldatetime`|SQLDATETIM4|  
|`decimal`|SQLDECIMAL|  
|`numeric`|SQLNUMERIC|  
|`float`|SQLFLT8|  
|`real`|SQLFLT4|  
|`int`|SQLINT|  
|`bigint`|SQLBIGINT|  
|`smallint`|SQLSMALLINT|  
|`tinyint`|SQLTINYINT|  
|`money`|SQLMONEY|  
|`smallmoney`|SQLMONEY4|  
|`bit`|SQLBIT|  
|`uniqueidentifier`|SQLUNIQUEID|  
|`sql_variant`|SQLVARIANT|  
|`timestamp`|SQLBINARY|  
|UDT（用户定义的数据类型）|SQLUDT|  
  
 <sup>1</sup>格式存储在字符中的数据文件使用`char`作为文件存储类型。 因此，对于字符数据文件，SQLCHAR 是唯一出现在格式化文件中的数据类型。  
  
 <sup>2</sup>你无法进行大容量数据导入`text`， `ntext`，和`image`具有默认值的列。  
  
## <a name="additional-considerations-for-file-storage-types"></a>文件存储类型的其他注意事项  
 当您将数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例大容量导出到数据文件时：  
  
-   您始终可以指定 `char` 作为文件存储类型。  
  
-   如果输入的文件存储类型表示无效的隐式转换， **bcp**失败; 例如，不过您可以指定`int`有关`smallint`数据，如果指定`smallint`为`int`数据，导致溢出错误。  
  
-   当非字符数据类型（如 `float`、`money`、`datetime` 或 `int`）存储为其数据库类型时，数据将写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机格式的数据文件。  
  
    > [!NOTE]  
    >  在你以交互方式指定 **bcp** 命令中的所有字段后，该命令会提示你将自己对每个字段的响应保存到一个非 XML 格式化文件中。 有关非 XML 格式文件的详细信息，请参阅[ 非 XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [使用 bcp 指定字段长度 (SQL Server)](specify-field-length-by-using-bcp-sql-server.md)   
 [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)   
 [使用 bcp 指定数据文件中的前缀长度 (SQL Server)](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
