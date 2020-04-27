---
title: 使用 Unicode 本机格式导入或导出数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1d115dacc53cb074080931c2ebad88dcaf1c68d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011569"
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>使用 Unicode 本机格式导入或导出数据 (SQL Server)
  当必须将信息从一个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装复制到另一个时，Unicode 本机格式非常有用。 为非字符数据使用本机格式可以节省时间，并消除与字符格式之间不必要的数据类型转换。 在使用不同代码页的服务器之间大容量传输数据时，为所有字符数据使用 Unicode 字符格式可以防止丢失任何扩展字符。 可以通过任何批量导入方法读取 Unicode 本机格式的数据文件。  
  
 通过使用包含扩展字符或 DBCS 字符的数据文件在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的多个实例之间大容量传输数据时，建议使用 Unicode 本机格式。 对于非字符数据，Unicode 本机格式使用本机（数据库）数据类型。 对于字符数据（如 `char`、`nchar`、`varchar`、`nvarchar`、`text`、`varchar(max)`、`nvarchar(max)` 和 `ntext`），Unicode 本机格式使用 Unicode 字符数据格式。  
  
 在 Unicode 本机格式数据文件中存储为 SQLVARIANT 的 `sql_variant` 数据的运算方式与在本机格式数据文件中的运算方式相同，只是 `char` 和 `varchar` 值需转换为 `nchar` 和 `nvarchar`，这使得受影响列的存储量加倍。 这些值的原始元数据被保留，当大容量导入到表列时，这些值将转换回其原始的 `char` 和 `varchar` 数据类型。  
  
## <a name="command-options-for-unicode-native-format"></a>Unicode 本机格式的命令选项  
 可以使用**bcp**、BULK INSERT 或 INSERT ... 将 Unicode 本机格式数据导入表中选择\* "从 OPENROWSET （BULK ...）"。对于**bcp**命令或 BULK INSERT 语句，可以在命令行中指定数据格式。 对于 INSERT ...SELECT * FROM OPENROWSET(BULK...) 语句，必须在格式化文件中指定数据格式。  
  
 下列选项支持 Unicode 本机格式：  
  
|Command|选项|描述|  
|-------------|------------|-----------------|  
|**bcp**|**-N**|使**bcp**实用工具使用 Unicode 本机格式，该格式对所有非字符数据使用本机（数据库）数据类型，为`char`所有字符（、 `nchar`、 `varchar`、 `nvarchar` `text`、和`ntext`）数据使用 unicode 字符数据格式。|  
|BULK INSERT|DATAFILETYPE **= '** widenative **'**|大容量导入数据时使用 Unicode 本机格式。|  
  
 有关详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md)、[BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式化文件中为每个字段指定格式设置。 有关详细信息，请参阅 [用来导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
## <a name="examples"></a>示例  
 下列示例演示如何使用 **bcp** 批量导出本机数据以及使用 BULK INSERT 批量导入相同数据。  
  
### <a name="sample-table"></a>示例表  
 下列示例要求 **dbo** 架构下的 **AdventureWorks** 示例数据库中存在名称为 **myTestUniNativeData** 的表。 必须先创建此表，才能运行这些示例。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestUniNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要填充此表并查看得到的内容，请执行以下语句：  
  
```  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>使用 bcp 大容量导出本机数据  
 若要将表中数据导出到数据文件，请将 **bcp** 与 **out** 选项和以下限定符结合使用：  
  
|限定符|说明|  
|----------------|-----------------|  
|**-N**|指定本机数据类型。|  
|**-T**|指定 **bcp** 实用工具通过使用集成安全性的受信任连接连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，则需要指定 **-U** 和 **-P** 才能成功登录。|  
  
 以下示例将本机格式的数据从 `myTestUniNativeData` 表大容量导出到名为 `myTestUniNativeData-N.Dat` 的新数据文件中。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入：  
  
```  
bcp AdventureWorks..myTestUniNativeData out C:\myTestUniNativeData-N.Dat -N -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>使用 BULK INSERT 大容量导入本机数据  
 以下示例使用 BULK INSERT 将 `myTestUniNativeData-N.Dat` 数据文件中的数据导入到 `myTestUniNativeData` 表中。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestUniNativeData   
    FROM 'C:\myTestUniNativeData-N.Dat'   
   WITH (DATAFILETYPE='widenative');   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData;  
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
