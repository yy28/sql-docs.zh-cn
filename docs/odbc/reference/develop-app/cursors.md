---
title: 游标 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c0c6ae5b9bda276bcd1296fcb475063fea6db204
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="cursors"></a>游标
应用程序会获取与数据*光标*。 一种不同于结果集： 结果集是与特定搜索条件匹配的行集，而一种软件，将返回这些行到应用程序。 名称*游标，*因为它应用到数据库，可能源自终端的计算机上闪烁的光标。 就像该游标指示当前位置屏幕和类型化的单词出现的位置下一步，结果集上的光标指示结果集和下一步将返回哪些行中的当前位置。  
  
 ODBC 中的游标模型基于嵌入式 SQL 中的游标模型。 这些模型之间的一个显著区别是打开方式游标。 在嵌入式 SQL 中，光标必须显式声明并打开然后才能使用。 ODBC 中, 创建结果集的语句执行时隐式打开一个游标。 当打开游标时，它位于结果集的第一行之前。 在嵌入式 SQL 和 ODBC，应用程序使用它完毕后，必须关闭游标。  
  
 不同的游标有不同的特征。 最常见的一种称为的游标*只进游标，*结果集可以仅向前移动。 若要返回上一行，应用程序必须关闭并重新打开游标，然后从结果集直至到达所需的行的开头阅读行。 只进游标提供快速使结果集一次传递机制。  
  
 只进游标是不太适用于基于屏幕的应用程序，在其中用户向后滚动和前进到的数据。 此类应用程序可以通过读取结果集后，缓存本地的数据和执行滚动本身使用只进游标。 但是，这也仅适用于少量数据。 更好的解决方案是使用*可滚动游标，*以便进行随机访问结果集。 此类应用程序还可以提高性能的一次读取一行以上的数据使用所谓*阻止光标。* 有关块状游标的详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 只进游标是 ODBC 中的默认游标类型，并在以下各节中讨论。 有关块游标和可滚动游标的详细信息，请参阅[块状游标](../../../odbc/reference/develop-app/block-cursors.md)和[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  提交或回滚事务，通过显式调用**SQLEndTran**或通过在自动提交模式下操作时，会导致某些数据源，以关闭的连接上的所有语句上的所有游标。 有关详细信息，请参阅中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 属性[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
