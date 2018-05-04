---
title: 接口一致性级别 |Microsoft 文档
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
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8463905b55d4cde00fa3025607c5dafa0f0c20bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="interface-conformance-levels"></a>界面一致性级别
调配的目的是通知应用程序哪些功能可用于向其驱动程序中。 基于函数的均衡方案不足够实现此目标。 在 ODBC 3。*x*，驱动程序是否已分类基于它们具有的功能。 支持该功能可以包括支持函数;它还包括支持通过返回的信息类型描述符字段、 语句属性、"Y"值**SQLGetInfo**，依次类推。  
  
 若要简化的接口一致性的规范，ODBC，请定义三个一致性级别。 为了满足特定的一致性级别，驱动程序必须满足所有该一致性级别的要求。 符合给定级别意味着完整符合所有较低的级别。  
  
 一致性级别执行不始终划分为多整齐 ODBC 函数的特定列表的支持，但指定支持的功能，如以下部分中列出。 若要为一项功能提供支持，驱动程序必须支持对某些 ODBC 函数的调用的某些或所有窗体 (有关详细信息，请参阅[函数一致性](../../../odbc/reference/develop-app/function-conformance.md))，设置某些属性 (请参阅[属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md))，和某些描述符字段 (请参阅[描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md))。  
  
 应用程序通过连接到数据源并调用发现驱动程序的接口一致性级别**SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 选项。  
  
 驱动程序可用于实现它们声明完整的一致性级别以外的功能。 应用程序发现任何此类的其他功能，通过调用**SQLGetFunctions** （若要确定哪些 ODBC 函数有） 和**SQLGetInfo** （若要查询各种其他 ODBC 功能）。  
  
 有三种 ODBC 接口一致性级别： 核心、 级别 1 和级别 2。  
  
> [!NOTE]  
>  这些一致性级别有不同的要求与 ODBC 2 中的相同名称的 ODBC API 一致性级别 *.x*。 具体而言，所有功能都隐含 ODBC 2 *.x* API 一致性级别 1 现在是核心接口一致性级别的一部分。 因此，许多 ODBC 驱动程序可能会报告核心级别接口的一致性。  
  
 本部分包含以下主题。  
  
-   [核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函数一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
