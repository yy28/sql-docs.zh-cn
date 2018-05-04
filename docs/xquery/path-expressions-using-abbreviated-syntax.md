---
title: 使用缩写在路径表达式中的语法 |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9751d48c38ae96f85d0cc97992f5dd5acfef9b2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="path-expressions---using-abbreviated-syntax"></a>路径表达式-使用缩写的语法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  中的所有示例[了解 XQuery 中的路径表达式](../xquery/path-expressions-xquery.md)使用路径表达式的缩写的语法。 路径表达式中用于轴步骤的未缩写语法包括轴名称和节点测试（用双冒号分隔），后跟零或更多个步骤限定符。  
  
 例如：  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery 支持在路径表达式中使用下列缩写：  
  
-   **子**轴是默认轴。 因此，**子::** 轴可以省略从表达式中的步骤。 例如，`/child::ProductDescription/child::Summary` 可以写为 `/ProductDescription/Summary`。  
  
-   **属性**轴可缩写为@。 例如，`/child::ProductDescription[attribute::ProductModelID=10]` 可以写为 `/ProudctDescription[@ProductModelID=10]`。  
  
-   A **/descendant-or-self::node()/** 可缩写为 / /。 例如，`/descendant-or-self::node()/child::act:telephoneNumber` 可以写为 `//act:telephoneNumber`。  
  
     上一个查询检索了存储在 Contact 表的 AdditionalContactInfo 列中的所有电话号码。 AdditionalContactInfo 的架构定义的方式， \<telephoneNumber > 元素可以在文档中的任意位置出现。 因此，若要检索所有电话号码，必须搜索文档中的每一个节点。 从文档的根节点开始搜索，接下来搜索所有后代节点。  
  
     以下查询将检索某一特定客户的联系人的所有电话号码：  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="http://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     如果将路径表达式替换为缩写语法 `//act:telephoneNumber`，会收到相同的结果。  
  
-   **自助:: node （)** 在步骤中可缩写为一个句点 （.）。 但是，该点不等效也可以与**自助:: node （)**。  
  
     例如，在以下查询中，使用点表示的是一个值而不是节点：  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   **父:: node （)** 在步骤中可缩写为双句点 （.）。  
  
  
