---
title: 检查功能支持和可变性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47f16160c05d1c410e3889f0bb857befe88df5b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299167"
---
# <a name="checking-feature-support-and-variability"></a>检查功能支持和可变性
为了检查功能支持和可变性，应用程序通常调用**SQLGetInfo、SQLGet****函数**和**SQLGetTypeInfo**。 一个好的起始位置是驱动程序的 API 和 SQL 语法符合性级别。 这些描述了广泛的功能支持级别。 然后，应用程序可以调用**SQLGetInfo**与其他选项一起确定其需要的功能的支持或可变性 **，SQLGet函数**确定是否支持超出返回的一致性级别所需的功能，以及**SQLGetTypeInfo**来确定支持哪些 SQL 数据类型。  
  
 应用程序可以通过使用该属性调用**SQLSetStmtAttr**或**SQLSetConnectAttr**来确定语句或连接属性是否受支持。 如果函数返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，则属性受支持;如果函数返回该属性，则为该属性。如果它返回SQL_ERROR和 SQLSTATE HYC00（未实现可选功能），则不支持该属性。  
  
 应用程序还可以通过调用**SQLDriver**在连接到驱动程序之前确定有限的信息量。
