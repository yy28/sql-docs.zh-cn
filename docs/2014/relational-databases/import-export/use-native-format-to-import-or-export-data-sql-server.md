---
title: 使用本机格式导入或导出数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2e91899172dfc6d640df0c33c77e32de3c1c21c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011661"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>使用本机格式导入或导出数据 (SQL Server)
  当使用不包含任何扩展/双字节字符集 (DBCS) 字符的数据文件在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间大容量传输数据时，建议使用本机格式。  
  
> [!NOTE]  
>  若要使用包含扩展字符或 DBCS 字符的数据文件在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间大容量传输数据，应使用 Unicode 本机格式。 有关详细信息信息，请参阅 [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)。  
  
 本机格式保留数据库的本机数据类型。 本机格式适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表之间的高速数据传输。 如果使用格式化文件，则源表和目标表不必相同。 数据传输分为两个步骤：  
  
1.  将源表中的数据批量导出到数据文件中  
  
2.  将数据文件中的数据批量导入到目标表中  
  
 在相同的表之间使用本机格式避免了在各数据类型与字符格式之间进行不必要的转换，从而节省了时间和空间。 但是，若要获得最佳的传输速率，应执行几个有关数据格式的检查。 为了防止加载的数据出现问题，请参阅以下限制列表。  
  
## <a name="restrictions"></a>限制  
 若要成功导入本机格式的数据，请确保：  
  
-   数据文件是本机格式的文件。  
  
-   目标表必须与数据文件（含有正确的列数、数据类型、长度及 NULL 状态等）兼容，或者您必须使用格式化文件将每一个字段映射到其相应列。  
  
    > [!NOTE]  
    >  如果从与目标表不匹配的文件中导入数据，那么导入操作可能会成功，但插入到目标表中的数据值很可能是错误的。 这是由于文件中的数据是通过使用目标表的格式来解释的。 因此，任何不匹配都会导致插入错误值。 但是，这样的不匹配决不会导致数据库中出现逻辑或物理不一致。  
  
     有关使用格式化文件的信息，请参阅[用于导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
 成功的导入操作不会损坏目标表。  
  
## <a name="how-bcp-handles-data-in-native-format"></a>bcp 如何处理本机格式的数据  
 本节论述了 **bcp** 实用工具如何导出和导入本机格式数据的特殊注意事项。  
  
-   非字符数据  
  
     bcp 实用工具使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部二进制数据格式将表中的非字符数据写入数据文件中。  
  
-   `char` 数据或 `varchar` 数据  
  
     每个开头`char`或`varchar`字段中， **bcp**添加前缀长度。  
  
    > [!IMPORTANT]  
    >  当使用本机模式时，默认情况下， **bcp** 实用工具先将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的字符转换为 OEM 字符，然后将这些字符复制到数据文件中。 **bcp** 实用工具先将数据文件中的字符转换为 ANSI 字符，然后将这些字符大容量导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。 在执行这些转换过程中，可能丢失扩展字符数据。 对于扩展字符，请使用 Unicode 本机格式或指定代码页。  
  
-   `sql_variant` 数据  
  
     如果 `sql_variant` 数据以 SQLVARIANT 存储在本机格式数据文件中，则数据会保留其所有特征。 记录每个数据值的数据类型的元数据与数据值一起存储。 此元数据用于在目标 `sql_variant` 列中重新创建具有相同数据类型的数据值。  
  
     如果目标列的数据类型不是 `sql_variant`，则每个数据值将按照隐式数据转换的一般规则转换为目标列的数据类型。 如果在数据转换过程中出现错误，则回滚当前批。 在 `char` 列之间传输的任何 `varchar` 值和 `sql_variant` 值都可能存在代码页转换问题。  
  
     有关数据转换的详细信息，请参阅[数据类型转换（数据库引擎）](/sql/t-sql/data-types/data-type-conversion-database-engine)。  
  
## <a name="command-options-for-native-format"></a>本机格式的命令选项  
 你可以使用 **bcp**、BULK INSERT 或 INSERT ...将本机格式数据导入表选择\*从 OPENROWSET （BULK）。对于 **bcp** 命令或 BULK INSERT 语句，你可以在命令行中指定数据格式。 对于 INSERT ... SELECT * FROM OPENROWSET(BULK...) 语句，您必须在格式化文件中指定数据格式。  
  
 下列命令行选项支持本机格式：  
  
|Command|Option|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-n**|将导致**bcp**实用工具使用本机数据类型的数据。<sup>1</sup>|  
|BULK INSERT|DATAFILETYPE **='** native **'**|使用本机数据类型或宽本机数据类型的数据。 注意，如果格式化文件指定了数据类型，则不需要 DATAFILETYPE。|  
  
 <sup>1</sup>加载本机 ( **-n**) 到与早期版本的兼容的格式数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端，使用 **-V**切换。 有关详细信息，请参阅 [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)。  
  
 有关详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md)、[BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式化文件中为每个字段指定格式设置。 有关详细信息，请参阅 [用来导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
## <a name="examples"></a>示例  
 下列示例演示如何使用 **bcp** 批量导出本机数据以及使用 BULK INSERT 批量导入相同数据。  
  
### <a name="sample-table"></a>示例表  
 下列示例要求 **dbo** 架构下的 **AdventureWorks** 示例数据库中存在名为 **myTestNativeData** 的表。 必须先创建此表，才能运行这些示例。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要填充此表并查看得到的内容，请执行以下语句：  
  
```  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>使用 bcp 大容量导出本机数据  
 若要将表中数据导出到数据文件，请将 **bcp** 与 **out** 选项和以下限定符结合使用：  
  
|限定符|Description|  
|----------------|-----------------|  
|**-n**|指定本机数据类型。|  
|**-T**|指定 **bcp** 实用工具通过使用集成安全性的受信任连接连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，则需要指定 **-U** 和 **-P** 才能成功登录。|  
  
 以下示例将本机格式的数据从 `myTestNativeData` 表大容量导出到名为 `myTestNativeData-n.Dat` 的新数据文件中。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks..myTestNativeData out C:\myTestNativeData-n.Dat -n -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>使用 BULK INSERT 大容量导入本机数据  
 以下示例使用 BULK INSERT 将 `myTestNativeData-n.Dat` 数据文件中的数据导入到 `myTestNativeData` 表中。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestNativeData   
    FROM 'C:\myTestNativeData-n.Dat'   
   WITH (DATAFILETYPE='native');   
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [sql_variant (Transact-SQL)](/sql/t-sql/data-types/sql-variant-transact-sql)   
 [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
