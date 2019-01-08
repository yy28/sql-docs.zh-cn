---
title: 检索的数据类型使用 SQLGetTypeInfo 信息 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c69113e4bb5457cb997f832179e5c1aab2841d82
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518871"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>使用 SQLGetTypeInfo 检索数据类型信息
从基础 SQL 数据类型到 ODBC 类型标识符的映射是近似值，因为 ODBC 提供了一个函数 (**SQLGetTypeInfo**) 的驱动程序可以完全通过描述数据源中的每个 SQL 数据类型。 此函数返回结果集，其中每行描述了一种数据类型，例如名称、 类型标识符、 精度、 小数位数和为 null 性的特征。  
  
 此信息通常允许用户创建和更改表的通用应用程序使用。 此类应用程序调用**SQLGetTypeInfo**若要检索的数据类型信息，然后向用户显示的部分或全部。 此类应用程序需要注意两件事：  
  
-   多个 SQL 数据类型可以映射到单个类型标识符，这可以使难以确定要使用的数据类型。 若要解决此问题，结果集进行排序首先通过类型标识符和第二个类型标识符定义的程度。 此外，数据源定义数据类型优先于用户定义数据类型。 例如，假设数据源定义的是相同，不同之处在于计数器自动递增的整数和计数器的数据类型。 此外假设 WHOLENUM 的用户定义类型是整数的同义词。 每种类型将映射到 SQL_INTEGER。 在中**SQLGetTypeInfo**结果集，首先，跟 WHOLENUM 显示整数，然后计数器。 WHOLENUM 后面的整数，因为它是用户定义的但之前计数器，因为它的详细信息紧密匹配的 SQL_INTEGER 定义类型标识符。  
  
-   ODBC 不会定义中使用的数据类型名称**CREATE TABLE**并**ALTER TABLE**语句。 相反，应用程序应使用返回的结果集的 TYPE_NAME 列中返回的名称**SQLGetTypeInfo**。 这样做的原因是，虽然大部分 SQL 不会跨 Dbms 的很多不同，数据类型名称有很大差异。 而不是强制驱动程序分析 SQL 语句并将标准数据类型名称替换为特定于 DBMS 的数据类型名称时，ODBC 要求应用程序第一个位置中使用特定于 DBMS 的名称。  
  
 请注意， **SQLGetTypeInfo**不一定是描述的所有应用程序可能会遇到数据类型。 具体而言，结果集可能包含不直接支持的数据源的数据类型。 例如，由 ODBC 定义的目录函数返回的结果集中的列的数据类型和数据源可能不支持这些数据类型。 若要确定结果集中的数据类型的特征，应用程序调用**SQLColAttribute**。
