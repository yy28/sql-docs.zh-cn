---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e569e51540cbaa5612b158abdacac5faae77f940
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722625"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol 和 SQLColAttribute
**SQLDescribeCol**并**SQLColAttribute**用于检索结果集元数据。 这两个函数之间的差异在于**SQLDescribeCol**始终返回相同的五项信息 （列的名称、 数据类型、 精度、 小数位数和为 null 性），同时**SQLColAttribute**返回单个应用程序请求的信息片段。 但是， **SQLColAttribute**可以返回元数据，包括列的区分大小写一个丰富得多选择、 显示大小、 可更新性，以及可搜索性。  
  
 许多应用程序，尤其是那些仅显示数据，需要返回的元数据仅**SQLDescribeCol**。 对于这些应用程序，它是更快地使用**SQLDescribeCol**比**SQLColAttribute**因为单个调用中返回的信息。 其他应用程序，尤其是更新数据，需要返回的其他元数据**SQLColAttribute** ，因此使用这两个函数。 此外， **SQLColAttribute**支持驱动程序特定的元数据; 有关详细信息，请参阅[驱动程序特定数据类型、 描述符类型、 信息类型、 诊断类型和属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 应用程序可以在任何时间，并已准备或执行一个语句游标位于结果集已关闭后检索结果集元数据。 应用程序很少需要准备的语句后，在执行之前，结果集元数据。 如果可能，应等待应用程序来检索元数据之前，执行语句，因为某些数据源不能返回预定义语句的元数据和模拟驱动程序中此功能通常是一个缓慢的过程后。 例如，驱动程序可能会产生的零行结果集通过替换**其中**子句**选择**with 子句的语句**WHERE 1 = 2**和执行生成的语句。  
  
 元数据通常是相当昂贵从数据源检索的。 因此，驱动程序应缓存任何元数据，它们从服务器检索和保存的只要光标位于结果集处于打开状态。 此外，应用程序应请求仅在绝对需要的元数据。
