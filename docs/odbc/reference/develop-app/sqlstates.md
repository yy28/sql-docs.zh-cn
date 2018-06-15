---
title: SQLSTATEs |Microsoft 文档
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
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9408522a47b442e3001e09cdca2d636063f73fb5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913062"
---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTATEs 提供有关原因的警告或错误的详细的信息。 本手册中的 SQLSTATEs 基于这些在 ISO/IEF CLI 规范中，找到特定于 ODBC 开头 IM 这些 SQLSTATEs 虽然。  
  
 不同于的返回代码，本手册中的 SQLSTATEs 是指南，并驱动程序不需要返回它们。 因此，虽然驱动程序应返回任何错误或警告能够检测正确的 SQLSTATE，应用程序应不依靠始终发生。 这种情况的原因有两个方面：  
  
-   **不完整**; 尽管本手册列出大量的错误和警告和可能的原因，这些错误和警告，但它并不完整，并且可能不会是驱动程序实现只需改变太多。 任何给定的驱动程序可能不会返回所有 SQLSTATEs 本手册中列出，并可能会返回 SQLSTATEs 本手册中未列出。  
  
-   **复杂性**的某些数据库引擎-尤其是关系数据库引擎-返回按原义数千个错误和警告。 此类引擎的驱动程序不太可能映射所有这些错误和警告记录到 SQLSTATEs 工作量由于涉及到，映射的 inexactness、 生成的代码，大型大小和生成的代码，通常返回编程的低值在运行时应永远不会遇到的错误。 因此，驱动程序应映射尽可能多的错误和警告如看起来合理，并且请务必将这些错误和警告的哪些应用程序逻辑映射可能遵循，如 SQLSTATE 01004 （数据截断）。  
  
 因为 SQLSTATEs 不可靠地返回，因此大多数应用程序只需向其关联的诊断消息，通常适用于特定的错误或发生的警告，以及用户和本机错误代码显示它们。 因为应用程序不能使基于大多数 SQLSTATEs 的编程逻辑仍没有这样做中的功能很少任何丢失。 例如，假设**SQLExecDirect**返回 SQLSTATE 42000 （语法错误或访问冲突）。 如果导致此错误的 SQL 语句是硬编码或生成的应用程序，这是编程错误，该代码需要修复。 如果通过用户输入的 SQL 语句，这是用户错误，并在应用程序完成所有可通过通知用户的问题。  
  
 如果应用程序执行操作的编程逻辑基于 SQLSTATEs，它们应为 SQLSTATE 无法返回或不同的 SQLSTATE 要返回准备。 完全其可靠地返回 SQLSTATEs 可以基于仅与多个驱动程序的体验。 但是，一般原则是 SQLSTATEs 驱动程序或驱动程序管理器，而不是数据源中发生的错误会更容易可靠地返回。 例如，大多数驱动程序可能返回 SQLSTATE HYC00 （可选未实现的功能），而较少的驱动程序可能返回 SQLSTATE 42021 （列已存在）。  
  
 以下 SQLSTATEs 指示运行时错误或警告，并且是很好的候选对象，其为基础的编程逻辑。 但是，是没有保证的所有驱动程序将它们返回。  
  
-   01004 （截断的数据）  
  
-   01s02 的警告 （选项值已更改）  
  
-   HY008 （已取消的操作）  
  
-   HYC00 （未实现的可选功能）  
  
-   HYT00 （超时）  
  
 SQLSTATE HYC00 （未实现的可选功能） 很特别重要，因为它是在其中应用程序可以确定驱动程序是否支持特定语句或连接属性的唯一方法。  
  
 SQLSTATEs 和哪些函数都返回它们的完整列表，请参阅[附录 a: ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 每个函数可能会在其下返回特定 SQLSTATE 的条件的详细说明，请参阅该函数。
