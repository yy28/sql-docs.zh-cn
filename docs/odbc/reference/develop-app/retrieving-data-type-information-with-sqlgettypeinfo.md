---
title: 使用 SQLGetTypeInfo 检索数据类型信息 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec2bbba824eaf3d74133cf9754eca2593c9fb79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300057"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>使用 SQLGetTypeInfo 检索数据类型信息
由于从基础 SQL 数据类型到 ODBC 类型标识符的映射是近似的，因此 ODBC 提供了一个函数 （**SQLGetTypeInfo），** 驱动程序可以通过该函数完全描述数据源中的每个 SQL 数据类型。 此函数返回一个结果集，其中每行描述单个数据类型的特征，如名称、类型标识符、精度、缩放和 null。  
  
 通常，允许用户创建和更改表的通用应用程序可以使用此信息。 此类应用程序调用**SQLGetTypeInfo**来检索数据类型信息，然后将部分或全部信息呈现给用户。 此类应用程序需要了解两件事：  
  
-   多个 SQL 数据类型可以映射到单个类型标识符，这会使很难确定要使用的数据类型。 为了解决这个问题，结果集首先按类型标识符排序，第二个按与类型标识符定义的接近排序。 此外，数据源定义的数据类型优先于用户定义的数据类型。 例如，假设数据源将 INTEGER 和 COUNTER 数据类型定义为相同，但 COUNTER 是自动递增的。 还假设用户定义的类型"WHOLENUM"是 INTEGER 的同义词。 每种类型都映射到SQL_INTEGER。 在**SQLGetTypeInfo**结果集中，INTEGER 首先出现，然后是"反"， 然后是"反"。 在 INTEGER 之后出现，因为它是用户定义的，但在 COUNTER 之前，因为它更符合SQL_INTEGER类型标识符的定义。  
  
-   ODBC 不定义数据类型名称，用于**创建表**和**ALTER TABLE**语句。 相反，应用程序应使用**SQLGetTypeInfo**返回的结果集的TYPE_NAME列中返回的名称。 原因是，尽管大多数 SQL 在 DBMS 之间变化不大，但数据类型名称差异很大。 ODBC 要求应用程序首先使用特定于 DBMS 的名称，而不是强制驱动程序解析 SQL 语句并将标准数据类型名称替换为特定于 DBMS 的数据类型名称。  
  
 请注意 **，SQLGetTypeInfo**不一定描述应用程序可能遇到的所有数据类型。 特别是，结果集可能包含数据源不支持的数据类型。 例如，目录函数返回的结果集中的列的数据类型由 ODBC 定义，数据源可能不支持这些数据类型。 要确定结果集中数据类型的特征，应用程序调用**SQLColAttribute**。
