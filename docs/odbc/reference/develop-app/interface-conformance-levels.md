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
ms.openlocfilehash: 185e68ed8d083e3ccfbab99369f6a778766a4c09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138913"
---
# <a name="interface-conformance-levels"></a>接口一致性级别
进行调配的目的是通知应用程序可通过驱动程序使用哪些功能。 基于函数的分级方案无法充分实现此目标。 ODBC 3 中的。*x*，驱动程序根据其拥有的功能进行分类。 支持该功能可能包括支持函数;它还可以支持描述符字段、语句特性、 **SQLGetInfo**返回的信息类型的 "Y" 值，等等。  
  
 为了简化接口一致性规范，ODBC 定义了三个一致性级别。 为了满足特定的一致性级别，驱动程序必须满足该一致性级别的所有要求。 具有给定级别的一致性意味着完全符合所有较低级别。  
  
 一致性级别并不总是完全划分为支持特定的 ODBC 函数列表，而是指定支持的功能，如以下部分所列。 若要为某一功能提供支持，驱动程序必须支持对某些 ODBC 函数的部分或全部形式的调用（有关详细信息，请参阅[函数一致性](../../../odbc/reference/develop-app/function-conformance.md)），设置某些属性（请参阅[属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)）和某些描述符字段（请参阅[描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)）。  
  
 应用程序通过连接到数据源并使用 SQL_ODBC_INTERFACE_CONFORMANCE 选项调用**SQLGetInfo**来发现驱动程序的接口一致性级别。  
  
 驱动程序可以自由地在其宣称完成一致性的级别之外实现功能。 应用程序通过调用**SQLGetFunctions** （以确定存在的 odbc 函数）和**SQLGetInfo** （查询各种其他 odbc 功能）来发现任何此类其他功能。  
  
 有三个 ODBC 接口一致性级别：核心、级别1和级别2。  
  
> [!NOTE]
>  这些一致性级别的要求不同于 ODBC 2.x 中具有相同名称的 ODBC API 一致性*级别。* 特别是，ODBC*2.X API 一致性*级别1隐含的所有功能现在都属于核心接口一致性级别。 因此，许多 ODBC 驱动程序可能会报告核心级接口一致性。  
  
 本部分包含下列主题。  
  
-   [核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函数一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
