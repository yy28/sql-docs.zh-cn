---
title: "FOR JSON 如何将 SQL Server 数据类型转换为 JSON 数据类型 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 527cb99c5caf0bb805e17f3b77b7d5e017e28ace
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON 如何将 SQL Server 数据类型转换为 JSON 数据类型 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 子句在 JSON 输出中使用以下规则将 SQL Server 数据类型转换为 JSON 类型。  
  
|类别|SQL Server 数据类型|JSON 数据类型|  
|--------------|--------------|---------------|  
|字符和字符串类型|char、 nchar、 varchar、 nvarchar|string|  
|数字类型|int、bigint、float、decimal、numeric|number|  
|位类型|bit|布尔值（true 或 false）|  
|日期和时间类型|date、datetime、datetime2、time、datetimeoffset|string|  
|二进制类型|varbinary、binary、image、timestamp、rowversion|BASE64 编码的字符串|  
|CLR 类型|geometry、 geography、 其他 CLR 类型|不提供支持。 这些类型将返回错误。<br /><br /> 在 SELECT 语句中，使用 CAST 或 CONVERT，或使用 CLR 属性或方法，将源数据转换为可以成功转换为 JSON 类型的 SQL Server 数据类型。 例如，使用**stastext （)** geometry 类型，或使用**tostring （)**对任何 CLR 类型。 JSON 输出值的类型然后派生自返回类型的应用的 SELECT 语句中的转换。|  
|其他类型|uniqueidentifier、money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
  
## <a name="see-also"></a>另请参阅  
 [借助 FOR JSON 将查询结果的格式设置为 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

