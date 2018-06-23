---
title: 指定字段终止符和行终止符 (SQL Server) | Microsoft Docs
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
- bcp utility [SQL Server], terminators
- field terminators [SQL Server]
- data formats [SQL Server], terminators
- row terminators [SQL Server]
- terminators [SQL Server]
ms.assetid: f68b6782-f386-4947-93c4-e89110800704
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9730f5e59d302b95f892d4de2860f3f8a0b147f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138269"
---
# <a name="specify-field-and-row-terminators-sql-server"></a>指定字段终止符和行终止符 (SQL Server)
  对于字符数据字段，可选的终止字符允许在数据文件中使用“字段终止符”  标记每个字段的结尾，以及使用“行终止符” 标记每行的结尾。 终止字符是为读取数据文件的程序指明一个字段或行的结束位置和另一个字段或行的开始位置的一种方式。  
  
> [!IMPORTANT]  
>  使用本机格式或 Unicode 本机格式时，请使用长度前缀而不要使用字段终止符。 本机格式数据可能与终止符冲突，因为本机格式的数据文件是以 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部二进制数据格式存储的。  
  
## <a name="characters-supported-as-terminators"></a>可用作终止符的字符  
 **bcp** 命令、BULK INSERT 语句和 OPENROWSET 大容量行集提供程序支持多种字符作为字段终止符或行终止符，并始终查找每个终止符的第一个实例。 下表列出了支持的终止符字符。  
  
|终止字符|表示方法|  
|---------------------------|------------------|  
|选项卡|\t<br /><br /> 这是默认的字段终止符。|  
|换行符|\n<br /><br /> 这是默认的行终止符。|  
|回车符/换行符|\r|  
|反斜杠<sup>1</sup>|\\\|  
|Null 终止符 （不可见终止符）<sup>2</sup>|\0|  
|任何可打印的字符（控制字符是不可打印的，除空值、制表符、换行符和回车之外）|（*、A、t、l 等）|  
|最长可达 10 个可打印字符的字符串，包括上面列出的部分或全部终止符|（**\t\*\*、end、!!!!!!!!!!、\t—\n 等）|  
  
 <sup>1</sup> t、 n、 r、 0 和 \0' 字符使用反斜杠转义字符，以生成一个控制字符。  
  
 <sup>2</sup>即使空控制字符 (\0) 不是打印时可见的它是一个独特的字符数据文件中。 这表示使用空控制字符作为字段终止符或行终止符与根本没有字段终止符或行终止符是不同的。  
  
> [!IMPORTANT]  
>  如果数据中出现终止符字符，则它被视为终止符（而非数据），并且该字符后的数据被视为属于下一个字段或记录。 因此，请仔细选择您的终止符，以确保它们从未出现在您的数据中。 例如，如果数据中包含某个低代理项，则低代理项字段终止符并不是一个好的选择。  
  
## <a name="using-row-terminators"></a>使用行终止符  
 行终止符可以与最后一个字段的终止符相同。 但是，通常来说，非重复的终止符是很有用的。 例如，若要生成表格格式的输出，可用换行符 (\n) 终止每行的最后一个字段，并用制表符 (\t) 终止所有其他字段。 若要将每个数据记录放置在数据文件中的各自的行上，请指定 \r\n 组合作为行终止符。  
  
> [!NOTE]  
>  交互使用 **bcp** 并指定 \n（换行符）作为行终止符时， **bcp** 将自动以 \r（回车符）作为前缀，从而形成行终止符 \r\n。  
  
## <a name="specifying-terminators-for-bulk-export"></a>指定大容量导出的终止符  
 大容量导出时`char`或`nchar`数据，并想要使用非默认终止符时，您必须指定到终止符**bcp**命令。 可以用下列任一方式指定终止符：  
  
-   使用格式化文件逐个字段指定终止符。  
  
    > [!NOTE]  
    >  有关如何使用格式化文件的详细信息，请参阅[导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
-   不使用格式化文件，但有下列可选方式：  
  
    -   使用 **-t** 开关为行中的所有字段（除最后一个字段以外）指定行终止符，并使用 **-r** 开关指定行终止符。  
  
    -   使用字符格式开关 **-c** 或 **-w**（而不是 **-t** 开关）将字段终止符设置为制表符 \t。 这与指定 **-t**\t 的作用相同。  
  
        > [!NOTE]  
        >  如果指定了 **-n** （本机数据）或 **-N** （Unicode 本机）开关，则不会插入终止符。  
  
    -   如果交互 **bcp** 命令包含 **in** 或 **out** 选项，而不包含格式化文件开关 (**-f**) 或数据格式开关（**-n**、 **-c**、 **-w**或 **-N**），并且选择不指定前缀长度和字段长度，则每个字段的字段终止符的命令提示符默认为无：  
  
         `Enter field terminator [none]:`  
  
         通常，默认设置是适当的选择。 但是，对于`char`或`nchar`数据字段，请参阅下一节"使用终止符指南"。 有关在上下文中显示此提示符的示例，请参阅[在使用 bcp 时指定数据格式以获得兼容性 (SQL Server)](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)。  
  
        > [!NOTE]  
        >  在你以交互方式指定 **bcp** 命令中的所有字段后，该命令会提示你将自己对每个字段的响应保存到一个非 XML 格式化文件中。 有关非 XML 格式文件的详细信息，请参阅[非 XML 格式化文件 (SQL Server)](xml-format-files-sql-server.md)。  
  
### <a name="guidelines-for-using-terminators"></a>使用终止符指南  
 在某些情况下，终止符很有用`char`或`nchar`数据字段。 例如：  
  
-   对于数据文件中包含 null 值的数据列，将不会被导入到不能理解前缀长度信息的程序中。  
  
     包含 null 值的任何数据列都被认为是可变长度。 如果缺少前缀长度，则需要一个终止符来确定 null 字段的结尾，同时确保正确地解释数据。  
  
-   对于其空间只被许多行部分占用的固定长度的长列。  
  
     在这种情况下，指定一个终止符可以最大限度地减少存储空间，同时可以将字段视为可变长度字段。  
  
### <a name="examples"></a>示例  
 此示例使用字符格式将 `AdventureWorks``HumanResources.Department` 表中的数据批量导出至 `Department-c-t.txt` 数据文件，其中将逗号用作字段终止符，将换行符 (\n) 用作行终止符。  
  
 **bcp** 命令包含以下开关。  
  
|开关|Description|  
|------------|-----------------|  
|**-c**|指定将数据字段作为字符数据加载。|  
|**-t** `,`|指定逗号 (,) 作为字段终止符。|  
|**-r** \n|指定行终止符作为换行符。 这是默认的行终止符，因此将其指定为可选。|  
|**-T**|指定 **bcp** 实用工具通过使用集成安全性的受信任连接连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，则需要指定 **-U** 和 **-P** 才能成功登录。|  
  
 有关详细信息，请参阅 [bcp Utility](../../tools/bcp-utility.md)。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks.HumanResources.Department out C:\myDepartment-c-t.txt -c -t, -r \n -T  
```  
  
 这创建了 `Department-c-t.txt`，其中包含 16 条记录，每条记录有四个字段。 这些字段由逗号分隔。  
  
## <a name="specifying-terminators-for-bulk-import"></a>为大容量导入指定终止符  
 大容量导入 `char` 或 `nchar` 数据时，大容量导入命令必须识别数据文件中使用的终止符。 如何指定终止符依赖于大容量导入命令，如下所示：  
  
-   **bcp**  
  
     为导入操作指定终止符与为导出操作指定终止符的语法相同。 有关详细信息，请参阅本主题前面的“为大容量导出指定终止符”。  
  
-   BULK INSERT  
  
     使用下表中列出的限定符可以为格式化文件中的各个字段或为整个数据文件指定终止符。  
  
    |Qualifier|Description|  
    |---------------|-----------------|  
    |FIELDTERMINATOR **='*`field_terminator`*'**|指定用于字符和 Unicode 字符数据文件的字段终止符。<br /><br /> 默认的字段终止符是 \t（制表符）。|  
    |ROWTERMINATOR **='*`row_terminator`*'**|指定用于字符和 Unicode 字符数据文件的行终止符。<br /><br /> 默认的行终止符是 \n（换行符）。|  
  
     有关详细信息，请参阅 [BULK INSERT (Transact SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
     对于 OPENROWSET 大容量行集提供程序，仅可以在格式化文件中指定终止符（这是必需的，除大型对象数据类型以外）。 如果字符数据文件使用非默认终止符，则必须在格式化文件中定义该非默认终止符。 有关详细信息，请参阅[创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md) 和[使用格式化文件批量导入数据 (SQL Server)](use-a-format-file-to-bulk-import-data-sql-server.md)。  
  
     有关 OPENROWSET BULK 子句的详细信息，请参阅 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
### <a name="examples"></a>示例  
 本部分的示例将字符数据从上述示例中创建的 `Department-c-t.txt` 数据文件大容量导入到 `myDepartment` 示例数据库的 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 表中。 必须先创建此表，才能运行这些示例。 若要在 **dbo** 架构下创建此表，请在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中执行以下代码：  
  
```  
USE AdventureWorks;  
GO  
DROP TABLE myDepartment;  
CREATE TABLE myDepartment   
(DepartmentID smallint,  
Name nvarchar(50),  
GroupName nvarchar(50) NULL,  
ModifiedDate datetime not NULL CONSTRAINT DF_AddressType_ModifiedDate DEFAULT (GETDATE())  
);  
GO  
  
```  
  
#### <a name="a-using-bcp-to-interactively-specify-terminators"></a>A. 使用 bcp 交互指定终止符  
 以下示例使用 `Department-c-t.txt` 命令大容量导入 `bcp` 数据文件。 该命令与大容量导出命令使用相同的命令开关。 有关详细信息，请参阅本主题前面的“为大容量导出指定终止符”。  
  
 在 Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks..myDepartment in C:\myDepartment-c-t.txt -c -t , -r \n -T  
```  
  
#### <a name="b-using-bulk-insert-to-interactively-specify-terminators"></a>B. 使用 BULK INSERT 交互指定终止符  
 以下示例使用 `Department-c-t.txt` 语句大容量导入 `BULK INSERT` 数据文件，该语句使用了下表中所示的限定符。  
  
|选项|Attribute|  
|------------|---------------|  
|DATAFILETYPE **=`char`**|指定将数据字段作为字符数据加载。|  
|FIELDTERMINATOR **='**`,`**'**|将逗号 (`,`) 指定为字段终止符。|  
|ROWTERMINATOR **='**`\n`**'**|指定行终止符作为换行符。|  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下代码：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myDepartment FROM 'C:\myDepartment-c-t.txt'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      ROWTERMINATOR = '\n'  
);  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [使用 bcp 指定字段长度 (SQL Server)](specify-field-length-by-using-bcp-sql-server.md)   
 [使用 bcp 指定数据文件中的前缀长度 (SQL Server)](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [使用 bcp 指定文件存储类型 (SQL Server)](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  
