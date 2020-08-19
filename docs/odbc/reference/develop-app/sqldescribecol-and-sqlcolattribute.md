---
description: SQLDescribeCol 和 SQLColAttribute
title: SQLDescribeCol 和 SQLColAttribute |Microsoft Docs
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
ms.openlocfilehash: 2de375ea207e8e393fa36c9795ebf0e3ca5f428b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424499"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol** 和 **SQLColAttribute** 用于检索结果集元数据。 这两个函数之间的区别在于， **SQLDescribeCol** 始终返回 (列的名称、数据类型、精度、小数位数和可为 null 性) 的五部分信息，而 **SQLColAttribute** 返回应用程序请求的一条信息。 但是， **SQLColAttribute** 可能会返回更丰富的元数据，包括列的区分大小写、显示大小、可更新性和可搜索性。  
  
 许多应用程序（尤其是只显示数据的应用程序）只需要 **SQLDescribeCol**返回的元数据。 对于这些应用程序，使用 **SQLDescribeCol** 比 **SQLColAttribute** 的速度更快，因为在单个调用中返回信息。 其他应用程序（尤其是更新数据的应用程序）需要 **SQLColAttribute** 返回的其他元数据，因此可使用这两种函数。 此外， **SQLColAttribute** 还支持驱动程序特定的元数据;有关详细信息，请参阅 [驱动程序特定的数据类型、描述符类型、信息类型、诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 应用程序可以在准备或执行语句之后以及在关闭结果集上的游标之前，随时检索结果集元数据。 很少有应用程序在语句准备好后和执行之前需要结果集元数据。 如果可能，应用程序应等待检索元数据，直到执行语句为止，因为某些数据源不能返回预定义语句的元数据并在驱动程序中模拟此功能通常是一个较慢的进程。 例如，驱动程序可能会通过将**SELECT**语句的**WHERE**子句替换为**1 = 2**并执行生成的语句，来生成零行结果集。  
  
 从数据源中检索元数据通常成本高昂。 因此，只要打开结果集上的游标，驱动程序就应缓存从服务器检索的任何元数据，并将其保存。 此外，应用程序应该只请求其绝对需要的元数据。
