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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 866e84844c563f1289a23a598cbd980d9b3bc432
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169579"
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
  
 \* 此类型受本机支持。  
  
 <sup>1</sup> UDT 表示用户定义的类型。  
  
## <a name="exporting-using-v-80"></a>使用 –V 80 进行导出  
 当你使用大容量导出数据 **– V80**切换，请`nvarchar(max)`， `varchar(max)`， `varbinary(max)`，XML，并使用 4 个字节的前缀，如存储在纯模式下的 UDT 数据`text`， `image`，和`ntext`数据，而不是使用 8 个字节的前缀，这是默认设置[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更高版本。  
  
## <a name="copying-date-values"></a>复制日期值  
 **bcp** 将使用 ODBC 大容量复制 API。 因此，为了将日期值导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中， **bcp** 使用了 ODBC 日期格式 (*yyyy-mm-dd hh:mm:ss*[*.f...*])。  
  
 **Bcp**命令将使用 ODBC 默认格式的字符格式数据文件导出`datetime`和`smalldatetime`值。 例如，包含日期 `12 Aug 1998` 的 `datetime` 列将以字符串 `1998-08-12 00:00:00.000` 的形式大容量复制到数据文件中。  
  
> [!IMPORTANT]  
>  导入到的数据时`smalldatetime`字段使用**bcp**，请确保秒数值为 00.000，否则操作将失败。 `smalldatetime`数据类型仅包含最接近的分钟值。 BULK INSERT 和 INSERT ...SELECT * FROM OPENROWSET(BULK...) 在这种情况下不会失败，但会截断秒值。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 
  
## <a name="see-also"></a>请参阅  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [SQL Server 数据库引擎的向后兼容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST 和 CONVERT (Transact-SQL)](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
