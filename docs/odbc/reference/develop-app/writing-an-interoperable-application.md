---
title: 编写的可互操作的应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f24e50b7f6dd8b129a2777ce1132ec426b7ea182
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078985"
---
# <a name="writing-an-interoperable-application"></a>编写交互式应用程序
每当应用程序使用多个驱动程序对相同的代码，该代码必须是可在这些驱动程序之间的互操作。 在大多数情况下，这是一个简单的任务。 例如，用于提取与只进游标的行的代码是相同的所有驱动程序。 在某些情况下，这可以更加困难。 例如，若要构造 SQL 语句中使用的标识符的代码需要考虑标识符的大小写，用引号括起来，和的一部分、 两部分和三部分命名约定。  
  
 一般情况下，可互操作代码必须要适应支持的功能和功能可变性的问题。 *功能支持*指是否支持某一特定功能。 例如，并非所有 Dbms 都支持事务，并且可互操作代码必须正常工作而不考虑事务都支持。 *功能可变性*指的是变体支持特定功能的方式。 例如，在某些 Dbms 中的标识符开头和末尾的标识符在其他放置目录名称。  
  
 在设计时或在运行时，支持的功能和功能可变性可以处理应用程序。 若要在设计时处理功能支持和可变性，开发人员会查看目标 Dbms 和驱动程序，并确保相同的代码将在它们之间的互操作性。 这通常是具有较低或有限的互操作性的应用程序应对这些问题的方法。  
  
 例如，如果开发人员保证垂直应用程序会只使用四个特定 Dbms，并且每个这些 Dbms 支持事务，应用程序不需要代码来检查在运行时的事务支持。 它始终会假定事务是可用的由于设计时使用的决定只需四个 Dbms，其中每个支持事务。  
  
 若要在运行时处理功能支持和可变性，应用程序必须在运行时用于不同的功能的测试并执行相应操作。 这通常是高度可互操作应用程序应对这些问题的方法。 对于功能支持问题，这意味着编写使模拟功能不可用时的功能可选或编写代码的代码。 对于功能可变性问题，这意味着编写支持所有可能变体的代码。  
  
 本部分包含以下主题。  
  
-   [检查功能支持和可变性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [要监视的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
