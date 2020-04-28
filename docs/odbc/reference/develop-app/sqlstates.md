---
title: SQLSTATEs |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be4bca929b8d48c301c6e71917503387004a6ec5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299724"
---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTATEs 提供有关警告或错误原因的详细信息。 本手册中的 SQLSTATEs 基于在 ISO/IEF CLI 规范中找到的项，但以 IM 开头的 SQLSTATEs 特定于 ODBC。  
  
 不同于返回代码，本手册中的 SQLSTATEs 是准则，不需要驱动程序即可返回它们。 因此，尽管驱动程序应返回正确的 SQLSTATE，以确保它们能够检测到任何错误或警告，但应用程序不应计算此始终发生的情况。 出现这种情况的原因有两个：  
  
-   **不完整性**尽管这一手册列出了大量错误和警告以及这些错误和警告的可能原因，但它并不完整，并且可能永远不会发生;驱动程序实现简单变化太多。 任何给定的驱动程序可能不会返回本手册中列出的所有 SQLSTATEs，并且可能会返回本手册中未列出的 SQLSTATEs。  
  
-   **复杂性**某些数据库引擎-特别是关系数据库引擎-返回了上千个错误和警告。 此类引擎的驱动程序不太可能将所有这些错误和警告都映射到 SQLSTATEs，因为涉及到相关工作、映射的 inexactness、大大小的生成代码和生成的代码的低值（通常返回在运行时永远不会遇到的编程错误）。 因此，驱动程序应将尽可能多的错误和警告映射为合理的错误和警告，并确保将应用程序逻辑可能所基于的错误和警告映射到这些错误和警告，如 SQLSTATE 01004 （数据已截断）。  
  
 由于 SQLSTATEs 不能可靠地返回，因此大多数应用程序只会将它们连同关联的诊断消息一起显示给用户，这通常针对发生的特定错误或警告以及本机错误代码进行定制。 这种情况几乎不会造成任何功能损失，因为应用程序不能在大多数 SQLSTATEs 上基础编程逻辑。 例如，假设**SQLExecDirect**返回 SQLSTATE 42000 （语法错误或访问冲突）。 如果导致此错误的 SQL 语句是硬编码或由应用程序生成的，则这是一种编程错误，需要修复代码。 如果用户输入了 SQL 语句，则这是一个用户错误，应用程序通过通知用户此问题可以完成全部操作。  
  
 当应用程序在 SQLSTATEs 上编写编程逻辑的基础时，应准备好将 SQLSTATE 返回或返回不同的 SQLSTATE。 确切返回的 SQLSTATEs 只能基于大量驱动程序的经验。 但是，一般原则是，对于驱动程序或驱动程序管理器中发生的错误（与数据源相对），更有可能是可靠返回的 SQLSTATEs。 例如，大多数驱动程序可能返回 SQLSTATE HYC00 （未实现可选功能），而较少的驱动程序可能返回 SQLSTATE 42021 （列已经存在）。  
  
 下面的 SQLSTATEs 指示运行时错误或警告，是对编程逻辑进行编程的良好候选项。 但是，并不保证所有驱动程序都返回它们。  
  
-   01004（数据截断）  
  
-   01S02 （选项值已更改）  
  
-   HY008 （操作取消）  
  
-   HYC00 （未实现可选功能）  
  
-   HYT00 （超时已过期）  
  
 SQLSTATE HYC00 （未实现可选功能）特别重要，因为它是应用程序可用于确定驱动程序是否支持特定语句或连接属性的唯一方法。  
  
 有关 SQLSTATEs 及其返回的功能的完整列表，请参阅[附录 a： ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 有关每个函数可能返回特定 SQLSTATE 的条件的详细说明，请参阅该函数。
