---
title: 数据访问器函数 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- data-accessor functions [XQuery]
ms.assetid: 31bad04f-7c74-4773-9f83-612704fdd21c
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f70f14b553182c4f52d9c27ec0972fd3d5978026
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="data-accessor-functions"></a>数据取值函数
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本节中的主题介绍数据取值函数并提供相应的示例代码。  
  
## <a name="understanding-fndata-fnstring-and-text"></a>了解 fn:data()、fn:string() 和 text()  
 XQuery 有一个函数**fn:data()** 从节点，节点测试提取标量、 类型化值**text （)** 返回文本节点和函数**fn:string()** ，返回节点的字符串值。 它们的用法容易混淆。 以下是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中正确使用它们的准则。 XML 实例\<age > 12 \< /存留时间 > 出于演示的目的使用。  
  
-   非类型化的 XML：路径表达式 /age/text() 返回文本节点“12”。 函数 fn:data(/age) 返回字符串值“12”，fn:string(/age) 也是如此。  
  
-   类型化的 XML： 表达式 /age/text() 返回任何简单类型化的静态错误\<age > 元素。 另一方面，fn:data(/age) 返回整数 12。 fn:string(/age) 产生字符串“12”。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [字符串函数&#40;XQuery&#41;](../xquery/data-accessor-functions-string-xquery.md)  
  
-   [数据函数&#40;XQuery&#41;](../xquery/data-accessor-functions-data-xquery.md)  
  
## <a name="see-also"></a>另请参阅  
 [路径表达式&#40;XQuery&#41;](../xquery/path-expressions-xquery.md)  
  
  
