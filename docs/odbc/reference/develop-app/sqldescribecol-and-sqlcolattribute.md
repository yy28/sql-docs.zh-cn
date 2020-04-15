---
title: SQL描述科尔和 SQLCol 属性 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8bd21010908473e4216a02a504b2de25578d5c84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299757"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol**和**SQLColAttribute**用于检索结果集元数据。 这两个函数之间的区别是**SQLDescribeCol**始终返回相同的五条信息（列的名称、数据类型、精度、缩放和空值），而**SQLColAttribute**返回应用程序请求的单个信息段。 但是 **，SQLColAttribute**可以返回更丰富的元数据选择，包括列的区分大小、显示大小、高数据性和可搜索性。  
  
 许多应用程序，尤其是仅显示数据的应用程序，只需要**SQLDescribeCol**返回的元数据。 对于这些应用程序，使用**SQLDescribeCol**比**SQLColAttribute**更快，因为信息在单个调用中返回。 其他应用程序（尤其是更新数据的应用程序）需要**SQLColAttribute**返回的其他元数据，因此可以使用这两个函数。 此外 **，SQLColAttribute**支持特定于驱动程序的元数据;有关详细信息，请参阅[特定于驱动程序的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 应用程序可以在准备或执行语句后以及关闭结果集上的游标之前随时检索结果集元数据。 很少的应用程序在编写语句后和执行语句之前需要结果集元数据。 如果可能，应用程序应等待检索元数据，直到执行语句之后，因为某些数据源无法返回已准备的语句的元数据，并且在驱动程序中模拟此功能通常是一个缓慢的过程。 例如，驱动程序可以通过将**SELECT**语句的**WHERE**子句替换为子句 WHERE 1 = **2**并执行结果语句来生成零行结果集。  
  
 从数据源检索元数据通常成本高昂。 因此，驱动程序应缓存他们从服务器检索到的任何元数据，并按住它，只要结果集上的光标处于打开状态。 此外，应用程序应仅请求他们绝对需要的元数据。
