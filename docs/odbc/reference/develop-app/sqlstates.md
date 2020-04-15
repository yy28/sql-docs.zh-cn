---
title: SQLSTATEs |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299724"
---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTAT 提供有关警告或错误原因的详细信息。 本手册中的 SQLSTATE 基于 ISO/IEF CLI 规范中的 SQLSTAT，尽管以 IM 开头的 SQLSTAT 特定于 ODBC。  
  
 与返回代码不同，本手册中的 SQLSTAT 是指南，并且不需要驱动程序来返回它们。 因此，虽然驱动程序应返回正确的 SQLSTATE，以查找它们能够检测到的任何错误或警告，但应用程序不应始终依赖这种情况。 造成这种情况的原因有两个方面：  
  
-   **不完整**尽管本手册列出了大量错误和警告以及这些错误和警告的可能原因，但它不完整，可能永远不会是;驱动程序实现差异太大。 任何给定的驱动程序可能不会返回本手册中列出的所有 SQLSTATEs，并且可能会返回本手册中未列出的 SQLSTAT。  
  
-   **复杂性**某些数据库引擎（尤其是关系数据库引擎）会返回数千个错误和警告。 由于所涉及的工作量、映射的不准确性、生成的代码的大大小以及生成的代码的较低值，此类引擎的驱动程序不太可能将所有这些错误和警告映射到 SQLSTATE，这些错误和警告通常返回在运行时不应遇到的编程错误。 因此，驱动程序应映射尽可能多的错误和警告，似乎合理，并确保映射应用程序逻辑可能基于的错误和警告，如 SQLSTATE 01004（数据截断）。  
  
 由于 SQLStatEs 无法可靠地返回，因此大多数应用程序只是将它们与其关联的诊断消息一起显示给用户，该消息通常针对发生的特定错误或警告以及本机错误代码进行定制。 执行此操作时很少会丢失任何功能，因为应用程序无论如何都不能将编程逻辑基于大多数 SQLSTAT。 例如，假设**SQLExecDirect**返回 SQLSTATE 42000（语法错误或访问冲突）。 如果导致此错误的 SQL 语句是硬编码或由应用程序构建的，则这是一个编程错误，需要修复代码。 如果用户输入 SQL 语句，则这是用户错误，应用程序通过通知用户问题，完成了所有可能的事情。  
  
 当应用程序对 SQLSTATEs 执行基本编程逻辑时，应为不返回 SQLSTATE 或返回其他 SQLSTATE 做好准备。 准确返回哪些 SQLSTAT 可以仅基于具有众多驱动程序的经验。 但是，一般准则是，与数据源相比，驱动程序或驱动程序管理器中发生的错误的 SQLSTAT 更有可能可靠地返回。 例如，大多数驱动程序可能返回 SQLSTATE HYC00（可选功能未实现），而返回 SQLSTATE 42021（已存在列）的驱动程序可能较少。  
  
 以下 SQLSTATE 指示运行时错误或警告，并且是建立编程逻辑的良好候选项。 但是，不能保证所有驱动程序都返回它们。  
  
-   01004 （数据截断）  
  
-   01S02 （选项值已更改）  
  
-   HY008 （操作已取消）  
  
-   HYC00（未实现可选功能）  
  
-   HYT00（超时已过期）  
  
 SQLSTATE HYC00（未实现可选功能）特别重要，因为它是应用程序确定驱动程序是否支持特定语句或连接属性的唯一方法。  
  
 有关 SQLSTAT 的完整列表以及返回哪些函数，请参阅附录[A：ODBC 错误代码](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 有关每个函数可能返回特定 SQLSTATE 的条件的详细说明，请参阅该函数。
