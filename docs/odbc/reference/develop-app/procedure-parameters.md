---
title: 过程参数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35d43ca7cf6e603d7dabca9eacf1e026daa753b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306950"
---
# <a name="procedure-parameters"></a>过程参数
过程调用中的参数可以是输入、输入/输出或输出参数。 这与所有其他 SQL 语句中的参数不同，后者始终是输入参数。  
  
 输入参数用于将值发送到过程。 例如，假设"零件"表具有"零件 ID"、"说明"和"价格"列。 InsertPart 过程可能具有表中每列的输入参数。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 在**SQLExecDirect**或**SQLExecute**返回SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE或SQL_NO_DATA之前，驱动程序不应修改输入缓冲区的内容。 当**SQLExecDirect**或**SQLExecute**返回SQL_NEED_DATA或SQL_STILL_EXECUTING时，不应修改输入缓冲区的内容。  
  
 输入/输出参数既用于将值发送到过程，又从过程检索值。 使用与输入和输出参数相同的参数往往令人困惑，应避免使用。 例如，假设过程接受订单 ID 并返回客户的 ID。 这可以通过单个输入/输出参数进行定义：  
  
```  
{call GetCustID(?)}  
```  
  
 最好使用两个参数：订单 ID 的输入参数和客户 ID 的输出或输入/输出参数：  
  
```  
{call GetCustID(?, ?)}  
```  
  
 输出参数用于检索过程返回值并从过程参数中检索值;返回值的过程有时称为*函数*。 例如，假设刚才提到的**GetCustID**过程返回一个值，指示它是否能够找到订单。 在以下调用中，第一个参数是用于检索过程返回值的输出参数，第二个参数是用于指定订单 ID 的输入参数，第三个参数是用于检索客户 ID 的输出参数：  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驱动程序处理过程中输入和输入/输出参数的值与其他 SQL 语句中的输入参数不一样。 执行语句时，它们会检索绑定到这些参数的变量的值，并将它们发送到数据源。  
  
 执行语句后，驱动程序将输入/输出参数的返回值存储在绑定到这些参数的变量中。 在提取过程返回的所有结果并返回**SQLMore 结果**SQL_NO_DATA之前，不保证对这些返回的值进行设置。 如果执行语句会导致错误，则输入/输出参数缓冲区或输出参数缓冲区的内容将未定义。  
  
 应用程序调用**SQL 程序**以确定过程是否具有返回值。 它调用**SQL过程列**以确定每个过程参数的类型（返回值、输入、输入/输出或输出）。
