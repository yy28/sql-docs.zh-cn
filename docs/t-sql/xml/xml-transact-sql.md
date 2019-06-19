---
title: xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a61816e39947bede45fff894facab912617b49be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62859873"
---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  存储 XML 数据的数据类型。 可在列中或者 xml 类型的变量中存储 xml 实例   。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>参数  
 CONTENT  
 将 xml 实例限制为格式正确的 XML 片段  。 XML 数据的顶层可包含多个零或多个元素。 还允许在顶层使用文本节点。  
  
 这是默认行为。  
  
 DOCUMENT  
 将 xml 实例限制为格式正确的 XML 片段  。 XML 数据必须且只能有一个根元素。 不允许在顶层使用文本节点。  
  
 xml_schema_collection   
 XML 架构集合的名称。 若要创建类型化的 xml 列或变量，可选择指定 XML 架构集合名称  。 有关类型化和非类型化 XML 的详细信息，请参阅[类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="remarks"></a>Remarks  
 存储的 xml 数据类型表示实例大小不能超过 2 GB  。  
  
 CONTENT 和 DOCUMENT 方面仅应用于类型化的 XML。 有关详细信息，请参阅[类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
## <a name="examples"></a>示例  
  
```  
USE AdventureWorks;  
GO  
DECLARE @DemographicData xml (Person.IndividualSurveySchemaCollection);  
SET @DemographicData =  (SELECT TOP 1 Demographics FROM Person.Person);  
SELECT @DemographicData;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型转换（数据库引擎）](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 语言参考 (SQL Server)](../../xquery/xquery-language-reference-sql-server.md)  
  
  
