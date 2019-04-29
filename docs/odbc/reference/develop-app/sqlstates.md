---
title: SQLSTATEs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ad31d9fd07e0b9f7bdf633f8ed546331880787c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149040"
---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTATEs 提供原因有关的警告或错误的详细的信息。 本手册中的 SQLSTATEs 基于 ISO/IEF CLI 规范中的那些虽然使用 IM 启动这些 SQLSTATEs 是特定于 ODBC。  
  
 与不同的返回代码，本手册中的 SQLSTATEs 是指导原则，并驱动程序不需要将其返回。 因此，虽然驱动程序应返回正确的任何错误或警告所支持检测的 SQLSTATE，应用程序不应统计上始终发生。 这种情况的原因是两方面：  
  
-   **不完整**; 虽然本手册列出了大量的错误和警告和可能的原因，这些错误和警告，但它并不完整并且可能不会是驱动程序实现，只需改变太多。 任何给定的驱动程序可能不会返回所有 SQLSTATEs 本手册中列出，并且可能会返回 SQLSTATEs 本手册中未列出。  
  
-   **复杂性**某些数据库引擎-尤其是关系数据库引擎-返回数千个错误和警告。 此类引擎的驱动程序不太可能所有这些错误和警告记录到 SQLSTATEs 由于工作涉及的映射的 inexactness、 生成的代码，大型大小和生成的代码，通常返回编程的低值在运行时应永远不会遇到的错误。 因此，驱动程序应尽可能多的错误和警告似乎是合理并确保将这些错误和警告的应用程序逻辑上映射可能为基础，如 SQLSTATE 01004 （数据被截断）。  
  
 因为 SQLSTATEs 不可靠地返回，因此大多数应用程序只需为其关联的诊断消息，通常适用于特定错误或发生的警告，以及用户和本机错误代码显示它们。 因为应用程序不能基于编程逻辑大多数 SQLSTATEs 仍没有丢失很少任何在执行此操作，此功能。 例如，假设**SQLExecDirect**返回 SQLSTATE 42000 （语法错误或访问冲突）。 如果导致此错误的 SQL 语句是硬编码或生成的应用程序，这是一种编程错误，代码需要修复。 如果用户输入的 SQL 语句，则这是用户错误，应用程序已完成的所有可通过通知问题的用户。  
  
 当应用程序进行基本的编程逻辑上 SQLSTATEs 时，它们应不要返回的 SQLSTATE 或不同的 SQLSTATE 要返回准备。 完全的可靠地返回 SQLSTATEs 可以仅基于多个驱动程序的经验。 但是，一般准则是驱动程序或驱动程序管理器，而不是数据源中发生的错误的 SQLSTATEs 很有可能会可靠地返回。 例如，大多数驱动程序可能返回 SQLSTATE HYC00 （可选功能未实现），而较少的驱动程序可能返回 SQLSTATE 42021 （列已存在）。  
  
 以下 SQLSTATEs 指示运行时错误或警告，是基于编程逻辑的最佳候选项。 但是，是没有保证的所有驱动程序将其返回。  
  
-   01004 （数据被截断）  
  
-   01S02 （选项值已更改）  
  
-   HY008 （已取消的操作）  
  
-   HYC00 （未实现的可选功能）  
  
-   HYT00 （超时已过期）  
  
 SQLSTATE HYC00 （未实现的可选功能） 是一点非常重要，因为它是在其中应用程序可以确定驱动程序是否支持特定的语句或连接属性的唯一方法。  
  
 SQLSTATEs 和哪些函数返回它们的完整列表，请参阅[附录 a:ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 在其下的每个函数可能会返回特定 SQLSTATE 的条件的详细说明，请参阅该函数。
