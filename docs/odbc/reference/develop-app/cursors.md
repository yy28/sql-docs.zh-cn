---
title: 游标 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da899e4dc47daff03c31277b3edd4d9c642b87cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305288"
---
# <a name="cursors"></a>游标
应用程序用*游标*获取数据。 游标与结果集不同：结果集是匹配特定搜索条件的行集，而游标是将这些行返回到应用程序的软件。 名称*光标*（如适用于数据库）可能源自计算机终端上的闪烁光标。 正如该光标指示屏幕上的当前位置以及键入的单词接下来将出现的位置一样，结果集中的光标指示结果集中的当前位置以及接下来将返回的行。  
  
 ODBC 中的游标模型基于嵌入式 SQL 中的游标模型。 这些模型之间的一个显著区别是打开游标的方式。 在嵌入式 SQL 中，必须显式声明和打开游标，然后才能使用它。 在 ODBC 中，在执行创建结果集的语句时隐式打开游标。 打开光标时，光标位于结果集的第一行之前。 在嵌入式 SQL 和 ODBC 中，必须在应用程序完成使用后关闭游标。  
  
 不同的游标具有不同的特征。 最常见的游标类型称为*仅前进游标，* 只能通过结果集向前移动。 要返回到上一行，应用程序必须关闭并重新打开游标，然后从结果集的开头读取行，直到到达所需的行。 仅前游标提供了一种快速机制，用于通过结果集进行单个传递。  
  
 仅前游标对于基于屏幕的应用程序使用较少，用户在其中通过数据向后和向前滚动。 此类应用程序可以通过读取结果集一次、在本地缓存数据以及自行执行滚动来使用仅转发游标。 但是，这仅适用于少量数据。 更好的解决方案是使用*可滚动的游标，* 它提供对结果集的随机访问。 此类应用程序还可以通过使用所谓的*块游标*一次获取多行数据来提高性能。 有关块游标的详细信息，请参阅[使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 仅前游标是 ODBC 中的默认游标类型，在以下各节中讨论。 有关块游标和可滚动游标的详细信息，请参阅[块游标](../../../odbc/reference/develop-app/block-cursors.md)和[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  通过显式调用**SQLEndTran**或以自动提交模式操作来提交或回滚事务，会导致某些数据源关闭连接上所有语句上的所有游标。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明中SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR属性。
