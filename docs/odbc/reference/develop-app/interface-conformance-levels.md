---
title: 接口一致性级别 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74d4ceb4532ee09004f035958860833aef488aaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446684"
---
# <a name="interface-conformance-levels"></a>接口一致性级别
调配的目的是通知应用程序提供的功能的内容从驱动程序。 基于函数的均衡方案无法充分实现此目标。 在 ODBC 3。*x*，驱动程序的分类基于它们所拥有的功能。 支持该功能可包括支持函数;它还包括由返回的信息类型的支持的描述符字段、 语句属性、"Y"值**SQLGetInfo**，依次类推。  
  
 若要简化的接口一致性规范，ODBC 定义三个一致性级别。 若要满足特定的一致性级别，驱动程序必须满足的所有要求的一致性级别。 符合给定级别意味着完成符合所有较低级别。  
  
 一致性级别执行不始终划分为整齐地支持特定的 ODBC 函数列表，但指定支持的功能，如以下各节中列出。 若要为一项功能提供支持，驱动程序必须支持某些 ODBC 函数的调用的某些或所有窗体 (有关详细信息，请参阅[函数一致性](../../../odbc/reference/develop-app/function-conformance.md))，设置特定的属性 (请参阅[属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md))，和特定的描述符字段 (请参阅[描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md))。  
  
 应用程序通过连接到数据源并调用发现驱动程序的接口一致性级别**SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 选项。  
  
 驱动程序可以随意实施超过声称到完整的一致性级别的功能。 应用程序发现任何此类附加功能，通过调用**SQLGetFunctions** （用于确定哪些 ODBC 函数都存在） 和**SQLGetInfo** （用于查询各种其他 ODBC 功能）。  
  
 有三个 ODBC 接口一致性级别：核心、 级别 1 和级别 2。  
  
> [!NOTE]
>  这些一致性级别有不同的要求比 ODBC 2 中的相同名称的 ODBC API 一致性级别 *.x*。 具体而言，所有功能权限都隐含的 ODBC 2 *.x* API 一致性级别 1 现在是核心接口一致性级别的一部分。 因此，很多 ODBC 驱动程序可能会报告核心级别接口一致性。  
  
 本部分包含以下主题。  
  
-   [核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函数一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
