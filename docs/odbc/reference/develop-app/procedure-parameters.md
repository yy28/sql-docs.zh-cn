---
title: 过程参数 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306950"
---
# <a name="procedure-parameters"></a>过程参数
过程调用中的参数可以是输入、输入/输出或输出参数。 这不同于所有其他 SQL 语句中的参数，这些语句始终是输入参数。  
  
 输入参数用于将值发送到过程。 例如，假设 Parts 表中包含 PartID、Description 和 Price 列。 InsertPart 过程可能会为表中的每个列提供一个输入参数。 例如：  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 在**SQLExecDirect**或**SQLExecute**返回 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_NO_DATA 之前，驱动程序不能修改输入缓冲区的内容。 当**SQLExecDirect**或**SQLExecute**返回 SQL_NEED_DATA 或 SQL_STILL_EXECUTING 时，不应修改输入缓冲区的内容。  
  
 输入/输出参数用于将值发送到过程，并从过程检索值。 同时使用与 input 和 output 参数相同的参数会造成混淆，应避免这样做。 例如，假设某一过程接受订单 ID 并返回该客户的 ID。 可以使用单个输入/输出参数定义此参数：  
  
```  
{call GetCustID(?)}  
```  
  
 使用两个参数可能更好：订单 ID 的输入参数以及客户 ID 的输出或输入/输出参数：  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Output 参数用于检索过程的返回值，并从过程参数中检索值;返回值的过程有时称为*函数*。 例如，假设刚才提到的**GetCustID**过程返回一个值，该值指示它是否能够查找顺序。 在下面的调用中，第一个参数是一个输出参数，用于检索过程返回值，第二个参数是用于指定顺序 ID 的输入参数，第三个参数是用于检索客户 ID 的输出参数：  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 驱动程序在过程中处理输入和输入/输出参数的值，而不是其他 SQL 语句中的输入参数。 执行语句时，它们会检索绑定到这些参数的变量的值，并将它们发送到数据源。  
  
 执行语句之后，驱动程序将输入/输出和输出参数的返回值存储在绑定到这些参数的变量中。 在提取了过程返回的所有结果并将**SQLMoreResults**返回 SQL_NO_DATA 之前，不一定要设置这些返回值。 如果执行语句导致错误，则输入/输出参数缓冲区或输出参数缓冲区的内容不确定。  
  
 应用程序调用**SQLProcedure**来确定过程是否具有返回值。 它调用**SQLProcedureColumns**来确定每个过程参数的类型（返回值、输入、输入/输出或输出）。
