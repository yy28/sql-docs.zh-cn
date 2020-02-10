---
title: 批量导入数据时保留标识值 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bb2fbd3129475c5d712cd4d1fce8bbe29ea096f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011906"
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>批量导入数据时保留标识值 (SQL Server)
  包含标识值的数据文件可以大容量导入到的实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。 默认情况下，将忽略导入的数据文件中标识列的值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动分配唯一值。 这些唯一值基于在表创建期间指定的种子和增量值。  
  
 如果该数据文件表中的标识符列不包含值，则使用格式化文件来指定导入数据时应跳过表中的标识符列。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动为此列分配唯一值。  
  
 若要防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在将数据行大容量导入到表中时分配标识值，请使用相应的保留标识命令限定符。 在您指定保留标识限定符后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在该数据文件中使用标识值。 这些限定符如下：  
  
|Command|保留标识限定符|限定符类型|  
|-------------|------------------------------|--------------------|  
|`bcp`|**-E**|开关|  
|BULK INSERT|KEEPIDENTITY|参数|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|表提示|  
  
 有关详细信息，请参阅 [bcp 实用工具](../../tools/bcp-utility.md)、[BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)、[OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)、[INSERT (Transact-SQL)](/sql/t-sql/statements/insert-transact-sql)、[SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql) 和[表提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-table)。  
  
> [!NOTE]  
>  要创建一个可在多个表中使用的自动递增数字或者可以从应用程序中调用而不引用任何表的自动递增数字，请参阅[序列号](../sequence-numbers/sequence-numbers.md)。  
  
## <a name="examples"></a>示例  
 本主题中的示例使用 INSERT .。。SELECT * FROM OPENROWSET （BULK ...）并保留默认值。  
  
### <a name="sample-table"></a>示例表  
 大容量导入实例需要在 **dbo** 架构下的 **AdventureWorks** 示例数据库中创建一个名为 **myTestKeepNulls** 的表。 创建该表。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行以下语句：  
  
```  
USE AdventureWorks;  
GO  
SELECT * INTO HumanResources.myDepartment   
   FROM HumanResources.Department  
      WHERE 1=0;  
GO  
SELECT * FROM HumanResources.myDepartment;  
```  
  
 作为 ** 基础的 **Department`myDepartment` 表的 IDENTITY_INSERT 设置为 OFF。 因此，必须指定 KEEPIDENTITY 或 **-E**，才能将数据导入标识列。  
  
### <a name="sample-data-file"></a>示例数据文件  
 大容量导入示例中使用的数据文件包含从本机格式的 `HumanResources.Department` 表中大容量导出的数据。 若要创建数据文件，请在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示符下输入以下内容：  
  
```  
bcp AdventureWorks.HumanResources.Department out myDepartment-n.Dat -n -T  
```  
  
### <a name="sample-format-file"></a>示例格式化文件  
 此大容量导入示例使用 XML 格式化文件 `myDepartment-f-x-n.Xml`，该文件使用本机数据格式。 此示例使用 `bcp` 进行创建，以从 `HumanResources.Department` 数据库的 `AdventureWorks` 表生成此格式化文件。 在 Windows 命令提示符下，输入以下内容：  
  
```  
bcp AdventureWorks.HumanResources.Department format nul -n -x -f myDepartment-f-n-x.Xml -T  
```  
  
 有关创建格式化文件的详细信息，请参阅[创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)。  
  
### <a name="a-using-bcp-and-keeping-identity-values"></a>A. 使用 bcp 并保留标识值  
 下面的示例说明如何在使用 `bcp` 大容量导入数据时保留标识值。 
  `bcp` 命令使用格式化文件 `myDepartment-f-n-x.Xml`，并包含下列开关：  
  
|限定符|说明|  
|----------------|-----------------|  
|**-E**|指定标识列使用数据文件中的标识值。|  
|**-T**|指定`bcp`实用工具使用可信连接连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到。|  
  
 在 Windows 命令提示符下输入。  
  
```  
bcp AdventureWorks.HumanResources.myDepartment in C:\myDepartment-n.Dat -f C:\myDepartment-f-n-x.Xml -E -T  
  
```  
  
### <a name="b-using-bulk-insert-and-keeping-identity-values"></a>B. 使用 BULK INSERT 并保留标识值  
 下面的示例使用 BULK INSERT 将数据从 `myDepartment-c.Dat` 文件大容量导入到 `AdventureWorks.HumanResources.myDepartment` 表中。 该语句使用 `myDepartment-f-n-x.Xml` 格式化文件，并包含 KEEPIDENTITY 选项来确保保留数据文件中的所有标识值。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行：  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
BULK INSERT HumanResources.myDepartment  
   FROM 'C:\myDepartment-n.Dat'  
   WITH (  
      KEEPIDENTITY,  
      FORMATFILE='C:\myDepartment-f-n-x.Xml'  
   );  
GO  
SELECT * FROM HumanResources.myDepartment;  
  
```  
  
### <a name="c-using-openrowset-and-keeping-identity-values"></a>C. 使用 OPENROWSET 并保留标识值  
 下面的示例使用 OPENROWSET 大容量行集提供程序将数据从 `myDepartment-c.Dat` 文件大容量导入到 `AdventureWorks.HumanResources.myDepartment` 表中。 该语句使用 `myDepartment-f-n-x.Xml` 格式化文件，并包含 KEEPIDENTITY 提示来确保保留数据文件中的所有标识值。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查询编辑器中，执行：  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
  
INSERT INTO HumanResources.myDepartment  
   with (KEEPIDENTITY)  
   (DepartmentID, Name, GroupName, ModifiedDate)  
   SELECT *  
      FROM  OPENROWSET(BULK 'C:\myDepartment-n.Dat',  
      FORMATFILE='C:\myDepartment-f-n-x.Xml') as t1;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [在批量导入期间保留 Null 或使用默认值 (SQL Server)](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [准备用于大容量导出或导入的数据 &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **使用格式化文件**  
  
-   [创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式化文件将表列映射到数据文件字段 (SQL Server)](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [使用格式化文件跳过数据字段 (SQL Server)](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式化文件跳过表列 (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **使用数据格式进行批量导入或批量导出**  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字符格式导入或导出数据 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **在使用 bcp 时指定数据格式以获得兼容性**  
  
1.  [指定字段终止符和行终止符 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [使用 bcp &#40;SQL Server 指定数据文件中的前缀长度&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [使用 bcp &#40;SQL Server 指定文件存储类型&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [表提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
