---
title: 编写互操作应用程序 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078985"
---
# <a name="writing-an-interoperable-application"></a>编写交互式应用程序
每当应用程序对多个驱动程序使用相同的代码时，该代码必须可在这些驱动程序之间进行互操作。 在大多数情况下，这是一项简单的任务。 例如，使用只进游标提取行的代码对于所有驱动程序都是相同的。 在某些情况下，这可能比较困难。 例如，用于构造要在 SQL 语句中使用的标识符的代码需要考虑标识符大小写、引号和由三部分组成的命名约定。  
  
 通常，可互操作的代码必须应对功能支持和功能可变性问题。 *功能支持*指特定功能是否受支持。 例如，并非所有 Dbms 都支持事务，并且互操作代码必须正常工作，而不考虑事务支持。 *功能可变性*指的是特定功能的支持方式。 例如，目录名称放置在某些 Dbms 中的标识符开头，在其他 Dbms 中放置在标识符的末尾。  
  
 应用程序可以在设计时或运行时处理功能支持和功能变化。 若要在设计时处理功能支持和可变性，开发人员需要了解目标 Dbms 和驱动程序，并确保相同的代码可在它们之间互操作。 这通常是由于互操作性较低或受限的应用程序处理这些问题的方式。  
  
 例如，如果开发人员保证垂直应用程序只使用四个特定的 Dbms，并且每个 Dbms 都支持事务，则该应用程序不需要代码来检查运行时的事务支持。 由于设计时决定仅使用四个 Dbms （每个 Dbms 都支持事务），因此它始终可以使用事务。  
  
 若要在运行时处理功能支持和可变性，应用程序必须在运行时测试不同的功能，并相应地执行操作。 这通常是高度可互操作的应用程序处理这些问题的方式。 对于功能支持问题，这意味着编写代码，使功能成为可选的或编写在功能不可用时模拟功能的代码。 对于功能可变性问题，这意味着编写支持所有可能变体的代码。  
  
 本部分包含下列主题。  
  
-   [检查功能支持和可变性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [要监视的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
