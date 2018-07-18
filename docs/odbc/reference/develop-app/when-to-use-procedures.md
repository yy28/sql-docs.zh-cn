---
title: 何时使用过程 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbc53507bf2cdf3333e0d36763ad7ecf7d359155
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917372"
---
# <a name="when-to-use-procedures"></a>何时使用过程
有大量的使用过程的优点，所有基于这一事实使用过程的 SQL 语句将从移动应用程序数据源。 剩下的应用程序中是一个可互操作的过程调用。 这些优点包括：  
  
-   **性能**过程通常是执行 SQL 语句的最快方法。 如已准备好执行，该语句编译和在两个单独步骤中执行。 与不同的是准备好的执行，仅在运行时执行过程。 而是在不同时间进行编译。  
  
-   **业务规则**A*业务规则*是有关一家公司在其中执行业务的方式的规则。 例如，只有具有标题销售人员的人员可能有权添加新的销售订单。 将这些规则放置过程中，各个公司可以通过重写应用程序而无需修改应用程序代码调用的过程自定义垂直应用程序。 例如，一个顺序输入应用程序可能调用该过程**InsertOrder**具有固定数量的参数; 完全如何**InsertOrder**实现因公司而异。  
  
-   **Replaceability**与密切相关的放置过程中的业务规则是，可以无需重新编译应用程序替换过程。 如果业务规则更改公司已购买并安装了应用程序后，公司可以更改包含该规则的过程。 从应用程序的角度来看，未进行任何更改;它仍调用完成特定任务的特定过程。  
  
-   **特定于 DBMS 的 SQL**过程提供应用程序能够利用特定于 DBMS 的 SQL 和仍然可互操作的方法。 例如上 DBMS 支持在 SQL 中的流控制语句, 的过程可能会捕获和从错误中恢复时上不支持的流控制语句的 DBMS 的过程可能只返回错误。  
  
-   **过程后仍存在事务**上某些数据源，在连接上所有已准备的语句的访问计划时，会删除已提交或回滚事务。 通过将 SQL 语句放在过程中，这将永久地存储在数据源中，语句在事务仍然有效。 是否过程在中生存下来的已准备，部分已准备好，或 unprepared 的状态是特定于 DBMS 的。  
  
-   **独立开发**从应用程序的其余部分可以单独开发过程。 在大型公司而言，这可能会提供一种方法，以便进一步攻击的高度专业化程序员的技能。 换而言之，应用程序程序员可以编写用户界面代码和数据库程序员可以写入过程。  
  
 由垂直和自定义应用程序通常使用过程。 这些应用程序往往会执行固定的任务，并且可能在它们中的硬编码过程调用。 例如，一个顺序输入应用程序可能调用过程**InsertOrder**， **DeleteOrder**，**应在 UpdateOrder**，和**GetOrders**.  
  
 很少从泛型应用程序调用过程。 过程通常写入特定应用程序的上下文中执行的任务，因此无需使用到通用应用程序。 例如，电子表格具有无需调用**InsertOrder**刚刚提到的过程。 此外，通用应用程序不应构造过程在运行时以确保其达到提供语句执行速度更快;不只是速度要慢于已准备或直接执行，这可能还需要特定于 DBMS 的 SQL 语句。  
  
 与此异常是应用程序开发环境，其中通常提供一种程序员可以生成 SQL 语句执行过程，可能会提供一种程序员可以测试过程的方法的方法。 此类环境的调用**SQLProcedures**到列表可用过程和**SQLProcedureColumns**若要列出输入、 输入/输出和输出参数，该过程返回值和的列创建一个过程的任何结果集。 但是，此类过程必须开发事先上每个数据源;这样做需要特定于 DBMS 的 SQL 语句。  
  
 有三个主要缺点使用过程。 第一个是过程必须编写和编译的应用程序将与之运行每个 DBMS。 虽然这不是自定义应用程序问题，它可显著提高开发和设计来运行具有大量的 Dbms 的垂直应用程序的维护时间。  
  
 第二个缺点是，许多 Dbms 不支持过程。 同样，这是最有可能是垂直设计为使用大量的 Dbms 运行的应用程序的问题。 若要确定是否支持过程，应用程序调用**SQLGetInfo** SQL_PROCEDURES 选项。  
  
 第三个缺点，这是特别适用于应用程序开发环境，是 ODBC 未定义用于创建过程标准语法。 也就是说，尽管应用程序可以 interoperably 调用过程，但它们无法 interoperably 创建它们。
