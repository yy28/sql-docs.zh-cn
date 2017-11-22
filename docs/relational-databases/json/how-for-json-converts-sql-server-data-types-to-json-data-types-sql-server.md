---
title: "FOR JSON 如何将 SQL Server 数据类型转换为 JSON 数据类型 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 07/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d934c3ddaee2d87a0a4afa5f9df900f759a1ed7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON 如何将 SQL Server 数据类型转换为 JSON 数据类型 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 子句在 JSON 输出中使用以下规则将 SQL Server 数据类型转换为 JSON 类型。  
  
|类别|SQL Server 数据类型|JSON 数据类型|  
|--------------|--------------|---------------|  
|字符和字符串类型|char、nchar、varchar、nvarchar|string|  
|数字类型|int、bigint、float、decimal、numeric|number|  
|位类型|bit|布尔值（true 或 false）|  
|日期和时间类型|date、datetime、datetime2、time、datetimeoffset|string|  
|二进制类型|varbinary、binary、image、timestamp、rowversion|BASE64 编码的字符串|  
|CLR 类型|geometry、geography、其他 CLR 类型|不提供支持。 这些类型将返回错误。<br /><br /> 在 SELECT 语句中，使用 CAST 或 CONVERT，或使用 CLR 属性或方法，将源数据转换为可成功转换成 JSON 类型的 SQL Server 数据类型。 例如，对 geometry 类型使用 STAsText()，或对任何 CLR 类型使用 ToString()。 然后，JSON 输出值的类型将派生自 SELECT 语句中应用的转换的返回类型。|  
|其他类型|uniqueidentifier、money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解 SQL Server 中内置 JSON 支持的详细信息  
若要获取大量特定解决方案、用例和建议，请参阅 Microsoft 项目经理 Jovan Popovic 发表的 SQL Server 和 Azure SQL 数据库中的[内置 JSON 支持相关博客文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。
  
## <a name="see-also"></a>另请参阅  
 [借助 FOR JSON 将查询结果的格式设置为 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
