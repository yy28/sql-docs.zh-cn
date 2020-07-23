---
title: 游标（ODBC） |Microsoft Docs
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
ms.openlocfilehash: 3a7484de48edaecea56fc135ca3b803875f9557c
ms.sourcegitcommit: 08f331b6a5fe72d68ef1b2eccc5d16cb80c6ee39
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86977774"
---
# <a name="cursors"></a>游标
应用程序使用*游标*来提取数据。 游标不同于结果集：结果集是与特定搜索条件相匹配的行集，而游标是将这些行返回到应用程序的软件。 应用于数据库的名称*游标*可能源自计算机终端上闪烁的光标。 就像该游标指示屏幕上的当前位置以及键入的字词将显示在哪个位置时，结果集上的游标将指示结果集中的当前位置和接下来返回的行。  
  
 ODBC 中的游标模型基于嵌入式 SQL 中的游标模型。 这些模型之间的一个明显差异就是游标的打开方式。 在嵌入的 SQL 中，必须显式声明并打开游标，然后才能使用。 在 ODBC 中，当执行创建结果集的语句时，将隐式打开游标。 当游标打开时，它将定位在结果集的第一行之前。 在嵌入式 SQL 和 ODBC 中，游标在应用程序使用完后必须关闭。  
  
 不同的游标具有不同的特征。 最常见的游标类型（称为*只进游标）* 只能在结果集中向前移动。 若要返回到上一行，应用程序必须关闭并重新打开游标，然后从结果集的开头读取行，直至到达所需的行。 只进游标提供了一种快速的机制，用于通过结果集进行单次传递。  
  
 只进游标对于基于屏幕的应用程序不太有用，用户可以在其中向后滚动数据。 此类应用程序可以通过读取结果集来使用只进游标，将数据缓存在本地，并执行滚动。 但是，这仅适用于少量数据。 更好的解决方案是使用可*滚动游标，该游标*提供对结果集的随机访问。 此类应用程序还可以通过使用所谓的*块游标*，一次提取多行数据，从而提高性能。 有关块游标的详细信息，请参阅[使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 只进游标是 ODBC 中的默认游标类型，并在以下各节中进行了讨论。 有关块游标和可滚动游标的详细信息，请参阅[块游标](../../../odbc/reference/develop-app/block-cursors.md)和可[滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  通过显式调用**SQLEndTran**或在自动提交模式下操作来提交或回滚事务，导致某些数据源关闭连接上所有语句上的所有游标。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 属性。
