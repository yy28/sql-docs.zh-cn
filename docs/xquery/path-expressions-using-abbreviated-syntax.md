---
title: 使用缩写语法中的路径表达式 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7454eb815faf26248b4326487a833f0038f64c1e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698265"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>路径表达式 - 使用缩写语法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  中的所有示例[了解在 XQuery 路径表达式](../xquery/path-expressions-xquery.md)路径表达式中使用未缩写的语法。 路径表达式中用于轴步骤的未缩写语法包括轴名称和节点测试（用双冒号分隔），后跟零或更多个步骤限定符。  
  
 例如：  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery 支持在路径表达式中使用下列缩写：  
  
-   **子**轴是默认轴。 因此，**子::** 轴可以从表达式中的一个步骤中省略。 例如，`/child::ProductDescription/child::Summary` 可以写为 `/ProductDescription/Summary`。  
  
-   **特性**轴可缩写为@。 例如，`/child::ProductDescription[attribute::ProductModelID=10]` 可以写为 `/ProudctDescription[@ProductModelID=10]`。  
  
-   一个**descendant-or-self::node()/** 可缩写为 / /。 例如，`/descendant-or-self::node()/child::act:telephoneNumber` 可以写为 `//act:telephoneNumber`。  
  
     上一个查询检索了存储在 Contact 表的 AdditionalContactInfo 列中的所有电话号码。 AdditionalContactInfo 架构一种方法中定义的\<telephoneNumber > 元素可以在文档中任何位置出现。 因此，若要检索所有电话号码，必须搜索文档中的每一个节点。 从文档的根节点开始搜索，接下来搜索所有后代节点。  
  
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
  
-   **Self:: node （)** 在步骤中可缩写为单个点 （.）。 但是，圆点是不等效也能与之互换**self:: node （)**。  
  
     例如，在以下查询中，使用点表示的是一个值而不是节点：  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   **父:: node （)** 在步骤中可缩写为两点 （..）。  
  
  
