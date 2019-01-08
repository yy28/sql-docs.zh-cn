---
title: 相对和绝对滚动 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ba05cb9079514750cf087149bae476efe0d8d41
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510760"
---
# <a name="relative-and-absolute-scrolling"></a>相对和绝对滚动
中的滚动选项的大多数**SQLFetchScroll**将光标置于相对于当前的位置或绝对位置。 **SQLFetchScroll**支持提取下一步，以前版本中，第一个和最后一个行集，作为也为相对提取 (提取行集*n*中当前行集的开始的行) 和绝对提取 （提取的行集起始在行*n*)。 如果*n*是负绝对提取中，行计数从结果集的末尾。 因此，绝对提取行-1 表示提取开头中的结果集的最后一行的行集。  
  
 动态游标检测到插入和删除从结果集中，因此没有简单的方法对于动态游标来检索结果集，这可能会很慢的开始处以外读取特定数量的行的行。 此外，绝对提取不是在动态游标中非常有用因为随着插入和删除行，将更改的行号因此，连续提取相同的行数可以产生不同的行。  
  
 使用的应用程序**SQLFetchScroll**仅对其块游标功能，如报表，有可能通过结果集一次，仅使用此选项提取下一步的行集。 基于屏幕的应用程序，但是，可以充分利用所有的功能**SQLFetchScroll**。 如果应用程序将行集大小设置为在屏幕上显示的行数，并将屏幕缓冲区绑定到结果集，它可以将滚动条操作直接向调用转换**SQLFetchScroll**。  
  
|滚动条操作|SQLFetchScroll 滚动选项|  
|--------------------------|-------------------------------------|  
|向上翻页|SQL_FETCH_PRIOR|  
|向下翻页|SQL_FETCH_NEXT|  
|向上移动一行|SQL_FETCH_RELATIVE *FetchOffset*等于-1|  
|向下移动一行|SQL_FETCH_RELATIVE *FetchOffset*等于 1|  
|在顶部的滚动框|SQL_FETCH_FIRST|  
|在底部的滚动框|SQL_FETCH_LAST|  
|滚动框位于随机位置|SQL_FETCH_ABSOLUTE|  
  
 此类应用程序还需要滚动操作，这要求的当前行号和行数后放置滚动条。 将当前的行数的应用程序可以既跟踪的当前行号或调用**SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 属性来对其进行检索。  
  
 游标，这是结果的大小中的行数设置，可用作诊断标头的 SQL_DIAG_CURSOR_ROW_COUNT 字段。 此字段中的值定义之后才**SQLExecute**， **SQLExecDirect**，或**SQLMoreResult**已调用。 此计数可以是近似计数或进行确切计数，具体取决于驱动程序的功能。 可以通过调用确定驱动程序的支持**SQLGetInfo**游标属性的信息类型和检查是否 SQL_CA2_CRC_APPROXIMATE 或 SQL_CA2_CRC_EXACT 位返回的游标的类型。  
  
 对于动态游标从不支持的确切的行计数。 对于其他类型的游标，该驱动程序可以准确或近似行计数，但不是能同时支持。 如果该驱动程序支持既不准确，也不近似特定游标类型的行计数，SQL_DIAG_CURSOR_ROW_COUNT 字段包含到目前为止已提取的行数。 支持哪些驱动程序，无论**SQLFetchScroll**与*操作*的 SQL_FETCH_LAST 将导致该 SQL_DIAG_CURSOR_ROW_COUNT 字段包含的确切的行计数。
