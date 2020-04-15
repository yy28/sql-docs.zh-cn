---
title: 接口一致性级别 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff555324746fcb92641126ddf11ea91ce5e3f89
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304597"
---
# <a name="interface-conformance-levels"></a>接口一致性级别
平平的目的是通知应用程序驱动程序中可以使用哪些功能。 基于函数的平配方案不能充分实现这一目标。 在 ODBC 3 中。*x*，驱动程序根据他们拥有的功能进行分类。 支持该功能可以包括支持该功能;它还可以包括支持描述符字段、语句属性 **、SQLGetInfo**返回的信息类型的"Y"值等。  
  
 为了简化接口一致性的规范，ODBC 定义了三个一致性级别。 为了满足特定的一致性级别，驱动程序必须满足该符合性级别的所有要求。 与给定级别的一致性意味着与所有较低级别完全一致。  
  
 一致性级别并不总是整齐地划分为对特定 ODBC 函数列表的支持，而是指定以下各节中列出的受支持的功能。 要支持某项功能，驱动程序必须支持对某些 ODBC 函数的部分或全部调用（有关详细信息，请参阅[函数一致性](../../../odbc/reference/develop-app/function-conformance.md)）、设置某些属性（请参阅[属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)）和某些描述符字段（请参阅[描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)）。  
  
 应用程序通过连接到数据源并调用**SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 选项来发现驱动程序的接口一致性级别。  
  
 驱动程序可以自由地实现超出其声明完全一致性的级别。 应用程序通过调用**SQLGet 函数**（确定存在哪些 ODBC 函数）和**SQLGetInfo（** 以查询各种其他 ODBC 功能）来发现任何此类附加功能。  
  
 有三个 ODBC 接口一致性级别：核心、级别 1 和级别 2。  
  
> [!NOTE]
>  这些符合性级别与 ODBC 2 *.x*中的同名 ODBC API 符合性级别的要求不同。 特别是，ODBC 2 *.x* API 符合性级别 1 所隐含的所有功能现在都是核心接口一致性级别的一部分。 因此，许多 ODBC 驱动程序可能会报告核心级接口的一致性。  
  
 本部分包含以下主题。  
  
-   [核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函数一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
