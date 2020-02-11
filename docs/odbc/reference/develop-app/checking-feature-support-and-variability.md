---
title: 检查功能支持和可变性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21495e538a554a477336d1a92926c11fe762c5af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062664"
---
# <a name="checking-feature-support-and-variability"></a>检查功能支持和可变性
若要检查功能支持和可变性，应用程序通常会调用**SQLGetInfo**、 **SQLGetFunctions**和**SQLGetTypeInfo**。 好的起点是驱动程序的 API 和 SQL 语法一致性级别。 它们描述了各种级别的功能支持。 然后，应用程序可以与其他选项一起调用**SQLGetInfo** ，以确定其所需功能的支持或可变性， **SQLGetFunctions**确定是否支持所需的超出返回的一致性级别的函数，以及**SQLGETTYPEINFO**以确定支持的 SQL 数据类型。  
  
 应用程序可以通过使用该属性调用**SQLSetStmtAttr**或**SQLSetConnectAttr**来确定是否支持语句或连接属性。 如果函数返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，则支持特性;如果它返回 SQL_ERROR 和 SQLSTATE HYC00 （可选功能未实现），则不支持该特性。  
  
 在通过调用**SQLDrivers**连接到驱动程序之前，应用程序还可以确定有限数量的信息。
