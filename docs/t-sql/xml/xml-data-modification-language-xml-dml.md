---
title: "XML 数据修改语言 (XML DML) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18fb5825297754c59f2824b6f05150ddaed7bb9c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="xml-data-modification-language-xml-dml"></a>XML 数据修改语言 (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML 数据修改语言 (XML DML) 是 XQuery 语言的扩展。 根据 W3C 的定义，XQuery 语言缺少数据操作 (DML) 部分。 在本主题中，以及 XQuery 语言中，引入 XML DML 提供完全正常运行的查询和数据修改语言，你可以使用针对**xml**数据类型。  
  
 XML DML 将下列区分大小写的关键字添加到 XQuery 中：  
  
-   **插入**  
  
-   **删除**  
  
-   **替换值**  
  
 中所述[XML 数据类型和列 &#40;SQL server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md)，你可以创建的变量和列**xml**键入并向它们分配 XML 文档或片段。 若要修改或更新这些 XML 实例，请执行下列操作：  
  
-   使用[modify （) 方法 xml 数据类型)](../../t-sql/xml/modify-method-xml-data-type.md)的**xml**数据类型。  
  
-   指定适当的 XML DML 语句内**modify （)**方法。  
  
 请注意，存在某些无法插入、删除或修改其值的属性。 例如：  
  
-   为类型化或非类型化**xml，**的属性将**xmlns**， **xmlns:\***，和**xml:base**。  
  
-   对于类型化**xml**仅，这些属性包括**xsi: nil**，和**xsi: type**。  
  
 下面列出了其他限制：  
  
-   为类型化或非类型化**xml**，这样的属性插入**xml:base**将失败。  
  
-   对于类型化**xml**、 删除和修改**xsi: nil**属性将会失败。 为非类型化**xml**，您可以删除该属性或修改其值。  
  
-   对于类型化**xml**，修改的值**xs:type**属性将会失败。 为非类型化**xml**，你可以修改的属性值。  
  
 修改类型化的 XML 实例时，最终格式必须是该类型的有效实例。 否则，将返回一个验证错误。  
  
## <a name="see-also"></a>另请参阅  
 [insert &#40;XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)   
 [删除 &#40;XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)   
 [替换值的 &#40;XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
