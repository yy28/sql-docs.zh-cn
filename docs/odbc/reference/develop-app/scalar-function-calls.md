---
description: 标量函数调用
title: 标量函数调用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6d0f77adaf6284bceac126b3539121cbdb174ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465585"
---
# <a name="scalar-function-calls"></a>标量函数调用
标量函数为每行返回一个值。 例如，绝对值标量函数使用数值列作为参数，并返回该列中每个值的绝对值。 用于调用标量函数的转义序列是  
  
 **{fn**  _标量函数_ **}**  
  
 其中， *标量函数* 是 [附录 E：标量函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)中列出的函数之一。 有关标量函数转义序列的详细信息，请参阅附录 C： SQL 语法中的 [标量函数转义序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) 。  
  
 例如，以下 SQL 语句创建了一个大写的客户名称的结果集。 第一条语句使用转义序列语法。 第二个语句使用适用于 OS/2 的 Ingres 的本机语法，并且不可互操作。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 应用程序可将调用混合到使用本机语法和调用使用 ODBC 语法的标量函数的标量函数。 例如，假定 Employee 表中的名称存储为姓氏、逗号和名字。 下面的 SQL 语句创建 Employee 表中雇员姓氏的结果集。 语句使用 ODBC 标量函数 **SUBSTRING** 和 SQL Server 标量函数 **CHARINDEX** 并仅在 SQL Server 上正确执行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 为了实现最大的互操作性，应用程序应使用 **CONVERT** 标量函数来确保标量函数的输出是所需的类型。 **CONVERT**函数将数据从一种 sql 数据类型转换为指定的 sql 数据类型。 **CONVERT**函数的语法是  
  
 **转换 (** _value_exp_ **，** _data_type_ **) **  
  
 其中*value_exp*是列名称，另一个标量函数的结果或文本值， *data_type*是一个关键字，该关键字与[附录 D：数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)中定义的 SQL 数据类型标识符所使用的 **#define**名称匹配。 例如，下面的 SQL 语句使用 **CONVERT** 函数来确保 **CURDATE** 函数的输出为日期，而不是时间戳或字符数据：  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 若要确定数据源支持哪些标量函数，应用程序需要使用 SQL_CONVERT_FUNCTIONS、SQL_NUMERIC_FUNCTIONS、SQL_STRING_FUNCTIONS、SQL_SYSTEM_FUNCTIONS 和 SQL_TIMEDATE_FUNCTIONS 选项来调用 **SQLGetInfo** 。 若要确定 **CONVERT** 函数支持哪些转换操作，应用程序将使用以 SQL_CONVERT 开头的任何选项调用 **SQLGetInfo** 。
