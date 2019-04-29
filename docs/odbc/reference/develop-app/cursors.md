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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91765f0572d8c880f7505948f7756b373fe28f62
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042123"
---
# <a name="cursors"></a>游标
应用程序提取使用数据*游标*。 光标位于不同于结果集：结果集是与特定搜索条件匹配的行集，而游标是返回的行应用程序的软件。 名称*游标，* 当其应用到数据库，可能源自终端的计算机上闪烁的光标。 就像该光标指示当前位置在屏幕上键入的词语将显示下一步，结果集的游标指示结果集和接下来将返回哪些行中的当前位置。  
  
 ODBC 中的游标模型基于的嵌入式 SQL 中的游标模型。 这些模型之间的一个显著区别是方式游标已打开。 在嵌入式 SQL 中，游标必须是显式声明和打开之前可以使用它。 在 ODBC 中，创建结果集的语句执行时隐式打开游标。 打开游标时，它被定位在结果集中的第一行之前。 在嵌入 SQL 和 ODBC，应用程序使用完后，必须关闭游标。  
  
 不同的游标有不同的特征。 最常见的游标类型，称为*只进游标*结果集可以仅向前移动。 若要返回上一行，应用程序必须关闭并重新打开游标，然后从结果集直到它达到所需的行的开头读取行。 只进游标提供快速机制可使经过结果集一次。  
  
 只进游标是不太适用于基于屏幕的应用程序，在用户滚动向后和向前浏览数据。 此类应用程序可以通过读取结果集后，缓存数据保存在本地，并执行滚动本身使用只进游标。 但是，这也仅适用于较少的数据。 更好的解决方案是使用*可滚动游标，* 以便进行随机访问的结果集。 此类应用程序还可以提高性能的一次提取多行数据使用的名称是什么*块游标。* 有关块游标的详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 只进游标是在 ODBC 中的默认游标类型和以下各节中讨论。 有关块游标和可滚动游标的详细信息，请参阅[块状游标](../../../odbc/reference/develop-app/block-cursors.md)并[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  提交或回滚事务，通过显式调用**SQLEndTran**或通过在自动提交模式下操作时，会导致某些数据源，以关闭上一个连接上的所有语句的所有游标。 有关详细信息，请参阅中的属性 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
