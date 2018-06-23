---
title: 使用 bcp 指定文件存储类型 (SQL Server) | Microsoft Docs
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
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 68630ac6e4a2ffad9079ed620e8d7d9660bf6381
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017940"
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>使用 bcp 指定文件存储类型 (SQL Server)
  “文件存储类型”  说明数据在数据文件中的存储方式。 可以将数据导出到数据文件为其数据库的表类型 （本机格式）、 字符表示形式 （字符格式），或为其中支持隐式转换; 任何数据类型例如，复制`smallint`作为`int`。 用户定义的数据类型将按其基类型导出。  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>用于文件存储类型的 bcp 提示符  
 如果某个交互式 **bcp** 命令包含不带格式化文件开关 ( **-f** ) 或数据格式开关（ **-n** 、**-c**、**-w**或 **-N**）的 **in**或 **out**选项，则该命令会提示输入每个数据字段的文件存储类型，如下所示：  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 您对此提示符的响应取决于要执行的任务，如下所示：  
  
-   若要以尽可能大的压缩存储的格式（本机数据格式）将数据从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例批量导出到数据文件中，请接受 **bcp**提供的默认文件存储类型。 有关本机文件存储类型的列表，请参阅本主题后面所述的“本机文件存储类型”。  
  
-   从实例大容量导出数据到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到采用字符格式数据文件，指定`char`作为表中的所有列的文件存储类型。  
  
-   大容量导入数据的实例到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从数据文件，将文件存储类型指定为`char`类型存储在字符格式，并且对于以本机数据类型格式存储的数据，指定文件存储类型之一，根据：  
  
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
  
     <sup>1</sup>字段长度、 前缀长度和终止符交互确定在导出为的非字符数据的数据文件中分配的存储空间量`char`文件存储类型。  
  
     <sup>2</sup> `ntext`， `text`，和`image`的未来版本中将删除数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在新的开发工作中，请避免使用这些数据类型，并修改当前使用它们的应用程序。 使用`nvarchar(max)`， `varchar(max)`，和`varbinary(max)`相反。  
  
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
  
 <sup>1</sup>存储的字符的数据文件格式使用`char`作为文件存储类型。 因此，对于字符数据文件，SQLCHAR 是唯一出现在格式化文件中的数据类型。  
  
 <sup>2</sup>你无法进行大容量导入数据到`text`， `ntext`，和`image`具有默认值的列。  
  
## <a name="additional-considerations-for-file-storage-types"></a>文件存储类型的其他注意事项  
 当您将数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例大容量导出到数据文件时：  
  
-   您始终可以指定 `char` 作为文件存储类型。  
  
-   如果您输入文件存储类型表示无效的隐式转换， **bcp**失败; 例如，尽管你可以指定`int`为`smallint`数据，如果你指定`smallint`为`int`数据，导致溢出错误。  
  
-   当非字符数据类型，如`float`， `money`， `datetime`，或`int`存储为其数据库类型，数据写入到中的数据文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机格式。  
  
    > [!NOTE]  
    >  在你以交互方式指定 **bcp** 命令中的所有字段后，该命令会提示你将自己对每个字段的响应保存到一个非 XML 格式化文件中。 有关非 XML 格式文件的详细信息，请参阅[ 非 XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [使用 bcp 指定字段长度 (SQL Server)](specify-field-length-by-using-bcp-sql-server.md)   
 [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)   
 [使用 bcp 指定数据文件中的前缀长度 (SQL Server)](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
