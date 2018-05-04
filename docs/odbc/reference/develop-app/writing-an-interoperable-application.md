---
title: 编写可互操作的应用程序 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7623f9e2674564a13061d144f599f974a3020a95
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="writing-an-interoperable-application"></a>编写可互操作的应用程序
每当应用程序使用针对多个驱动程序相同的代码，该代码必须在这些驱动程序之间的可互操作。 在大多数情况下，这是一个简单的任务。 例如，代码以提取与只进游标的行是相同的所有驱动程序。 在某些情况下，这可能更困难。 例如，用于构造 SQL 语句中使用的标识符的代码需要考虑标识符的大小写，用引号括起来，和一个部分、 两个部分构成和由三部分的命名约定。  
  
 一般情况下，可互操作的代码必须应对支持的功能，功能变化的问题。 *功能支持*指是否支持特定功能。 例如，并非所有 Dbms 都支持事务，并且可互操作的代码必须正常工作而不考虑事务都支持。 *功能变化*指的是支持特定功能的方式中的变体。 例如，放置的目录名称中某些 Dbms 的标识符开头和末尾的中其他的标识符。  
  
 在设计时或在运行时，支持的功能，功能变化可以处理应用程序。 若要在设计时处理支持的功能和变化，开发人员审视目标 Dbms 和驱动程序，并确保相同的代码将在它们之间的可互操作。 这通常是在其中具有低或有限的互操作性的应用程序处理这些问题的方法。  
  
 例如，如果开发人员可保证垂直的应用程序会仅使用四个特定 Dbms，并且每个这些 Dbms 支持事务，应用程序不需要代码，以检查在运行时的事务支持。 它始终可以假定事务是可用的因为设计时使用的决定只需四个 Dbms，其中每个支持事务。  
  
 若要在运行时处理支持的功能和变化，应用程序必须在运行时测试不同的功能，并采取相应的措施。 这通常是高度可互操作的应用程序应对这些问题的方法。 有关功能的支持问题，这意味着编写代码使模拟功能不可用时的功能可选或编写代码。 对于功能变化问题，这意味着编写支持所有可能变体的代码。  
  
 本部分包含以下主题。  
  
-   [检查功能支持和可变性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [要监视的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
