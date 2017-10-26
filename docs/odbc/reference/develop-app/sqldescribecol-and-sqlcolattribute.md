---
title: "SQLDescribeCol 和 SQLColAttribute |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a80ccf6ed695433a109770a567f50d100fd3a33
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol**和**SQLColAttribute**用于检索结果集元数据。 这两个函数之间的差异在于**SQLDescribeCol**始终返回相同五项时的信息 （列的名称、 数据类型、 精度、 小数位数和可为 null）， **SQLColAttribute**返回一段单独的请求的应用程序的信息。 但是， **SQLColAttribute**可以返回元数据，包括列的区分大小写的一个更丰富选择、 显示大小、 updatability，以及可搜索性。  
  
 许多应用程序，特别是，仅显示数据，需要返回的元数据仅**SQLDescribeCol**。 对于这些应用程序，它是更快地使用**SQLDescribeCol**比**SQLColAttribute**因为单次调用中返回的信息。 其他应用程序，特别更新数据，需要返回的其他元数据**SQLColAttribute** ，因此使用这两个函数。 此外， **SQLColAttribute**支持驱动程序特定的元数据; 有关详细信息，请参阅[特定于驱动程序的数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 应用程序可以在任何时间，并已准备或执行的语句游标位于结果集已关闭后检索结果集元数据。 很少的应用程序需要准备该语句后，在执行之前，结果集元数据。 如果可能，应等待应用程序以检索元数据之前之后执行该语句，因为某些数据源不能返回元数据已准备的语句和模拟驱动程序中的此功能通常是慢速的过程。 例如，该驱动程序可能会生成一个零行结果集，通过替换**其中**子句**选择**带有子句的语句**WHERE 1 = 2**和执行生成的语句。  
  
 元数据通常是相当昂贵从数据源中检索的。 因此，驱动程序应缓存任何元数据，它们从服务器检索和保存为只要设置游标位于结果上处于打开状态。 此外，应用程序应请求仅它们绝对需要的元数据。

