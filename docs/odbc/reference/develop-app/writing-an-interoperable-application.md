---
title: 编写可互操作的应用程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 553e718e0759e47701e7f8c04561693358d5dc52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289079"
---
# <a name="writing-an-interoperable-application"></a>编写交互式应用程序
每当应用程序对多个驱动程序使用相同的代码时，该代码必须在这些驱动程序之间互操作。 在大多数情况下，这是一个简单的任务。 例如，对于所有驱动程序，使用仅转发游标获取行的代码都相同。 在某些情况下，这可能更加困难。 例如，构造用于 SQL 语句的标识符的代码需要考虑标识符大小写、报价以及一部分、两部分和三部分命名约定。  
  
 通常，可互操作的代码必须处理功能支持和功能可变性问题。 *功能支持*是指是否支持特定功能。 例如，并非所有 DBMS 都支持事务，并且无论事务支持如何，可互操作的代码都必须正常工作。 *特征可变性*是指支持特定要素的方式变化。 例如，目录名称放置在某些 DBMS 中的标识符开头，并在其他 DBM 的标识符末尾放置。  
  
 应用程序可以在设计时或运行时处理功能支持和功能可变性。 为了在设计时处理功能支持和可变性，开发人员查看目标 DBMS 和驱动程序，并确保相同的代码在它们之间可互操作。 这通常是低或有限互操作性的应用程序处理这些问题的方式。  
  
 例如，如果开发人员保证垂直应用程序仅使用四个特定的 DBMS，并且如果每个 DBMS 都支持事务，则应用程序不需要代码来检查运行时的事务支持。 它始终可以假定事务可用，因为设计时决定仅使用四个 DBMS，每个 DBMS 都支持事务。  
  
 为了在运行时处理功能支持和可变性，应用程序必须在运行时测试不同的功能并相应地执行操作。 这通常是高度可互操作的应用程序处理这些问题的方式。 对于功能支持问题，这意味着编写使要素可选的代码或编写在功能不可用时模拟该功能的代码。 对于功能可变性问题，这意味着编写支持所有可能变体的代码。  
  
 本部分包含以下主题。  
  
-   [检查功能支持和可变性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [要监视的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
