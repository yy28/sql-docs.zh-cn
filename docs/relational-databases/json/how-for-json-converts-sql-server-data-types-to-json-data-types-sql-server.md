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
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c256bc9ecc0e518bb54d206a04f36d2b736500d8
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON 如何将 SQL Server 数据类型转换为 JSON 数据类型 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 子句在 JSON 输出中使用以下规则将 SQL Server 数据类型转换为 JSON 类型。  
  
|类别|SQL Server 数据类型|JSON 数据类型|  
|--------------|--------------|---------------|  
|字符和字符串类型|(n)(var)(char)|string|  
|数字类型|int、bigint、float、decimal、numeric|number|  
|位类型|bit|布尔值（true 或 false）|  
|日期和时间类型|date、datetime、datetime2、time、datetimeoffset|string|  
|二进制类型|varbinary、binary、image、timestamp、rowversion|BASE64 编码的字符串|  
|CLR 类型|CLR、geometry、geography|不提供支持。 这些类型将返回错误。<br /><br /> 在 SELECT 语句中，使用 CAST 或 CONVERT，或使用 CLR 属性或方法，将数据转换为可以转换成 JSON 类型的数据类型。 例如，对任何 CLR 类型都使用 **ToString()** ，或对几何类型使用 **stastext()** 。 JSON 输出值的类型派生自 SELECT 语句中使用的转换返回类型。|  
|其他类型|uniqueidentifier、money|string|  
  
## <a name="see-also"></a>另请参阅  
 [借助 FOR JSON 将查询结果的格式设置为 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

