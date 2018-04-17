---
title: 检索的数据类型信息与 SQLGetTypeInfo |Microsoft 文档
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
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e89297c8fb0cdd7cc048fd19a24810c67b2d271
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>检索 SQLGetTypeInfo 的数据类型信息
ODBC 基础 SQL 数据类型从到 ODBC 类型标识符的映射是近似值，因为提供函数 (**SQLGetTypeInfo**) 通过该驱动程序可以完全描述了每个数据源中的 SQL 数据类型。 此函数将返回一个结果集，其中每个行所说明的一种数据类型，例如名称、 类型标识符、 精度、 小数位数和可为 null 的特征。  
  
 此信息通常是由泛型应用程序允许用户创建和更改的表使用。 此类应用程序调用**SQLGetTypeInfo**检索数据类型信息以及然后向用户显示的部分或全部的它。 此类应用程序需要注意以下两个操作：  
  
-   多个 SQL 数据类型可以映射到单个类型标识符，这可以使难以确定哪种数据类型使用。 若要解决此问题，结果集进行排序首先通过类型标识符和第二个类型标识符定义到靠近程度。 此外，数据源定义数据类型的优先于用户定义的数据类型。 例如，假设数据源定义的整数和计数器数据类型必须相同，只不过计数器自动递增。 同时假定 WHOLENUM 用户定义的类型是整数的同义词。 上述每种类型映射到 SQL_INTEGER。 在**SQLGetTypeInfo**结果集，首先，跟 WHOLENUM 出现整数，然后计数器。 因为它是用户定义的但之前计数器由于它的详细信息密切匹配 SQL_INTEGER 的定义类型标识符，WHOLENUM 出现之后的整数。  
  
-   ODBC 未定义的在中使用的数据类型名称**CREATE TABLE**和**ALTER TABLE**语句。 相反，应用程序应使用在 TYPE_NAME 列中返回的结果集返回的名称**SQLGetTypeInfo**。 这样做的原因是，尽管大部分 SQL 不会跨 Dbms 的很多不同，数据类型名称有很大差异。 而不强制驱动程序以分析 SQL 语句和将标准数据类型名称替换为特定于 DBMS 的数据类型名称下 ODBC 需要应用程序首先使用特定于 DBMS 的名称。  
  
 请注意， **SQLGetTypeInfo**不一定描述所有应用程序可能会遇到的数据类型。 具体而言，结果集可能包含不直接支持的数据源的数据类型。 例如，由 ODBC 定义中由目录函数返回的结果集的列的数据类型和数据源可能不支持这些数据类型。 若要确定结果集中的数据类型的特征，应用程序调用**SQLColAttribute**。
