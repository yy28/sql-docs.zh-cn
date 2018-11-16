---
title: 本地-名称-从的 QName (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name-from-QName function
- local-name-from-QName function
ms.assetid: fafed718-8c3c-403f-93ee-ec51fc157a6e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 237db63c04d9b5a241bcabbca5a45e054da03118
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661936"
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>与 QName 相关的函数 - local-name-from-QName
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回表示指定的 QName 的本地部分 xs: ncname *$arg*。 结果是一个空序列，如果 *$arg*是空序列。  
  
## <a name="syntax"></a>语法  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 它是应从中提取本地名称的 QName。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
 下面的示例使用**local-name-from-qname （)** 函数来检索本地名称和命名空间 URI 部分从 QName 类型值。 该示例执行以下操作：  
  
-   创建 XML 架构集合。  
  
-   创建带有 xml 类型列的表。 xml 类型是使用 XML 架构集合类型化的。  
  
-   将示例 XML 实例存储到表中。 使用**query （)** 执行的查询表达式的 xml 数据类型的方法以从实例中检索 QName 类型值的本地名称部分。  
  
```sql
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<root xmlns="QNameXSD" xmlns:a="https://someURI">a:someLocalName</root>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare default element namespace "QNameXSD"; local-name-from-QName(/root[1])')  
FROM T  
-- Result = someLocalName  
-- You can retrieve namespace URI part from the QName using the namespace-uri-from-QName() function  
SELECT xmlCol.query('declare default element namespace "QNameXSD"; namespace-uri-from-QName(/root[1])')  
FROM T  
-- Result = https://someURI  
```  
  
## <a name="see-also"></a>请参阅  
 [与 Qname 相关的函数&#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
