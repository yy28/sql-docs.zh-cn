---
title: 用 SQLGetTypeInfo 检索数据类型信息 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300057"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>使用 SQLGetTypeInfo 检索数据类型信息
由于从基础 SQL 数据类型到 ODBC 类型标识符的映射是近似的，ODBC 提供了一个函数（**SQLGetTypeInfo**），通过该函数，驱动程序可以对数据源中的每个 SQL 数据类型进行完全描述。 此函数返回一个结果集，其中的每一行都描述了一种数据类型的特征，如名称、类型标识符、精度、小数位数和可为 null 性。  
  
 此信息通常由允许用户创建和更改表的通用应用程序使用。 此类应用程序会调用**SQLGetTypeInfo**来检索数据类型信息，然后向用户显示其部分或全部信息。 此类应用程序需要注意两个问题：  
  
-   多个 SQL 数据类型可以映射到单个类型标识符，这可能会导致难以确定要使用的数据类型。 若要解决此情况，结果集首先按类型 identifier 和 second 靠近程度到类型标识符的定义。 此外，数据源定义的数据类型优先于用户定义的数据类型。 例如，假设数据源将整数和计数器数据类型定义为相同，只不过该计数器是自动递增的。 假设用户定义类型 WHOLENUM 是整数的同义词。 其中每个类型都映射到 SQL_INTEGER。 在**SQLGetTypeInfo**结果集中，整数首先出现，后跟 WHOLENUM，then COUNTER。 WHOLENUM 在整数后出现，因为它是用户定义的，但在 COUNTER 之前，因为它与 SQL_INTEGER 类型标识符的定义更匹配。  
  
-   ODBC 不会定义要在**CREATE TABLE**和**ALTER TABLE**语句中使用的数据类型名称。 相反，应用程序应使用**SQLGetTypeInfo**返回的结果集的 TYPE_NAME 列中返回的名称。 这样做的原因是，尽管大多数 SQL 在 Dbms 上没有太大的差别，但数据类型名称差别很大。 ODBC 要求应用程序首先使用特定于 DBMS 的名称，而不是强制驱动程序分析 SQL 语句并将标准数据类型名称替换为 DBMS 特定的数据类型名称。  
  
 请注意， **SQLGetTypeInfo**并不一定说明应用程序可以遇到的所有数据类型。 具体而言，结果集可能包含数据源不直接支持的数据类型。 例如，目录函数返回的结果集中的列的数据类型由 ODBC 定义，数据源可能不支持这些数据类型。 若要确定结果集中数据类型的特征，应用程序将调用**SQLColAttribute**。
