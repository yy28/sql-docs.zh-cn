---
title: 导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- earlier versions [SQL Server], import and export data formats
- -V switch
- data formats [SQL Server], earlier versions
- previous versions [SQL Server], import and export data formats
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 274c984d6ecec8af8f5bea27496450a45fc2f1df
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026799"
---
# <a name="import-native-and-character-format-data-from-earlier-versions-of-sql-server"></a>导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，可以通过将 **bcp** 与 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-V [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]开关一起使用，从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 、 **或** 中导入本机和字符格式数据。 **-V** 开关将使 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早期版本中的数据类型，并且数据文件格式与早期版本中的格式相同。  
  
 若要为数据文件指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本，可将 **-V** 开关与以下的任一限定符一起使用：  
  
|SQL Server 版本|Qualifier|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## <a name="interpretation-of-data-types"></a>对数据类型的解释  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本均支持一些新的类型。 如果要将新的数据类型导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中，则必须以早期的 **bcp** 客户端可读的格式存储该数据类型。 下表总结了如何转换新数据类型以便与早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]兼容。  
  
|SQL Server 2005 中的新数据类型|版本 6*x*兼容的数据类型|版本 70 中兼容的数据类型|版本 80 中兼容的数据类型|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|`bigint`|`decimal`|`decimal`|*|  
|`sql_variant`|`text`|`nvarchar(4000)`|*|  
|`varchar(max)`|`text`|`text`|`text`|  
|`nvarchar(max)`|`ntext`|`ntext`|`ntext`|  
|`varbinary(max)`|`image`|`image`|`image`|  
|XML|`ntext`|`ntext`|`ntext`|  
|UDT<sup>1</sup>|`image`|`image`|`image`|  
  
 \*此类型受本机支持。  
  
 <sup>1</sup> UDT 表示用户定义的类型。  
  
## <a name="exporting-using--v-80"></a>使用 -V 80 进行导出  
 使用 **-V80**开关大容量导出数据时， `nvarchar(max)` 纯模式下的、、、 `varchar(max)` `varbinary(max)` XML 和 UDT 数据将存储为带有4个字节的前缀，例如 `text` 、 `image` 和 `ntext` 数据，而不是使用8字节前缀，这是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本的默认值。  
  
## <a name="copying-date-values"></a>复制日期值  
 **bcp** 将使用 ODBC 大容量复制 API。 因此，为了将日期值导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中， **bcp** 使用了 ODBC 日期格式 (*yyyy-mm-dd hh:mm:ss*[ *.f...* ])。  
  
 **Bcp**命令使用和值的 ODBC 默认格式导出字符格式的数据 `datetime` 文件 `smalldatetime` 。 例如，包含日期 `12 Aug 1998` 的 `datetime` 列将以字符串 `1998-08-12 00:00:00.000` 的形式大容量复制到数据文件中。  
  
> [!IMPORTANT]  
>  使用 bcp 将数据导入到字段中时 `smalldatetime` ，请确保秒数值为00.000，否则操作将失败。 **bcp** `smalldatetime` 数据类型仅支持最接近的分钟值。 BULK INSERT 和 INSERT ...SELECT * FROM OPENROWSET(BULK...) 在这种情况下不会失败，但会截断秒值。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 
  
## <a name="see-also"></a>另请参阅  
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [SQL Server 数据库引擎的向后兼容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST 和 CONVERT (Transact-SQL)](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
