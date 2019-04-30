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
manager: craigg
ms.openlocfilehash: b9af2cfd73556baca4870428cdcdfcee3e07191d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217612"
---
# <a name="checking-feature-support-and-variability"></a>检查功能支持和可变性
若要检查的功能支持和可变性，应用程序通常会调用**SQLGetInfo**， **SQLGetFunctions**，并**SQLGetTypeInfo**。 很好的起点是驱动程序的 API 和 SQL 语法一致性级别。 这些过程描述广泛级别的功能支持。 然后，应用程序可以调用**SQLGetInfo**与其他选项来确定的支持的功能需求，可变性**SQLGetFunctions**以确定是否在超出返回需要函数它支持的一致性级别，并**SQLGetTypeInfo**来确定支持哪些 SQL 数据类型。  
  
 应用程序可以确定是否通过调用支持的语句或连接属性**SQLSetStmtAttr**或**SQLSetConnectAttr**具有该属性。 如果该函数将返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，则支持该属性;如果它将返回 SQL_ERROR 和 SQLSTATE HYC00 （可选功能未实现），不支持的属性。  
  
 应用程序还可以确定将有限的数量的信息，然后连接到该驱动程序通过调用**SQLDrivers**。
