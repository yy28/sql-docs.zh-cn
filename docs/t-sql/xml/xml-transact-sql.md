---
title: "xml (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e85eb245cf9d53f7d38579928a5145828797002
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  存储 XML 数据的数据类型。 你可以存储**xml**中一列或变量的实例**xml**类型。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>参数  
 CONTENT  
 限制**xml**实例设置为格式正确的 XML 片段。 XML 数据的顶层可包含多个零或多个元素。 还允许在顶层使用文本节点。  
  
 这是默认行为。  
  
 DOCUMENT  
 限制**xml**实例设置为格式正确的 XML 文档。 XML 数据必须且只能有一个根元素。 不允许在顶层使用文本节点。  
  
 *xml_schema_collection*  
 XML 架构集合的名称。 若要创建类型化**xml**列或变量，你可以选择指定 XML 架构集合名称。 有关类型化和非类型化的 XML 的详细信息，请参阅[比较类型化的 XML 添加到非类型化 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="remarks"></a>注释  
 存储的表示形式**xml**数据类型实例不能超过 2 千兆字节 (GB) 的大小。  
  
 CONTENT 和 DOCUMENT 方面仅应用于类型化的 XML。 有关详细信息请参阅[比较类型化的 XML 添加到非类型化 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="examples"></a>示例  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @y xml (Sales.IndividualSurveySchemaCollection);  
SET @y =  (SELECT TOP 1 Demographics FROM Sales.Individual);  
SELECT @y;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 语言参考 (SQL Server)](../../xquery/xquery-language-reference-sql-server.md)  
  
  

