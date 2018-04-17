---
title: 过程参数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc40885f18679bdcaa36a40ee2fd27147d97ac6b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="procedure-parameters"></a>过程参数
在过程调用中的参数可作为输入、 输入/输出，或输出参数。 这是在所有其他 SQL 语句中，后者始终是输入的参数的参数不同。  
  
 输入的参数用于将值发送到该过程。 例如，假设部件表具有 PartID、 描述和价格的列。 InsertPart 过程可能具有输入的参数，为每个列，表中。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 驱动程序不应修改直到输入缓冲区的内容**SQLExecDirect**或**SQLExecute**返回 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_NO_DATA。 不应修改输入缓冲区的内容时**SQLExecDirect**或**SQLExecute**返回 SQL_NEED_DATA 或 SQL_STILL_EXECUTING。  
  
 输入/输出参数用于同时将值发送到过程并从过程中检索值。 使用相同的参数作为输入和输出参数往往是令人困惑，应当避免。 例如，假设一个过程接受一个订单 ID，并返回客户的 ID。 这可以使用单个输入/输出参数来定义：  
  
```  
{call GetCustID(?)}  
```  
  
 它可能会更好使用两个参数： 订单 ID 的输出或客户 ID 的输入/输出参数的输入的参数：  
  
```  
{call GetCustID(?, ?)}  
```  
  
 检索过程返回值并检索其值的过程自变量; 使用输出参数返回值的过程有时称为*函数*。 例如，假设**GetCustID**刚刚提到的过程返回一个值，该值指示是否已能够找到顺序。 在以下的调用中，第一个参数是一个用于检索过程返回值的输出参数，第二个参数是输入的参数用于指定订单 ID，第三个参数是一个用于检索客户 ID 的输出参数：  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驱动程序处理的输入值和输入/输出过程中的参数不不同于其他 SQL 语句中的输入参数。 它们时执行该语句，检索的变量的值绑定到这些参数并将它们发送到数据源。  
  
 执行该语句后，驱动程序绑定到这些参数的变量中存储的返回的值的输入/输出和输出参数。 这些返回值没有保证之后已提取过程返回的所有结果之前设置和**SQLMoreResults**已返回 SQL_NO_DATA。 如果执行的语句会导致出现错误，将不确定的输入/输出参数缓冲区或输出参数缓冲区的内容。  
  
 应用程序调用**SQLProcedure**以确定过程是否具有一个返回值。 它调用**SQLProcedureColumns**以确定每个过程参数的类型 （返回值，输入、 输入/输出，或输出）。
