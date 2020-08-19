---
description: 接口一致性级别
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb77ab0e77fc8a811acd956673a4ad4fe8664828
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424619"
---
# <a name="interface-conformance-levels"></a>接口一致性级别
进行调配的目的是通知应用程序可通过驱动程序使用哪些功能。 基于函数的分级方案无法充分实现此目标。 ODBC 3 中的。*x*，驱动程序根据其拥有的功能进行分类。 支持该功能可能包括支持函数;它还可以支持描述符字段、语句特性、 **SQLGetInfo**返回的信息类型的 "Y" 值，等等。  
  
 为了简化接口一致性规范，ODBC 定义了三个一致性级别。 为了满足特定的一致性级别，驱动程序必须满足该一致性级别的所有要求。 具有给定级别的一致性意味着完全符合所有较低级别。  
  
 一致性级别并不总是完全划分为支持特定的 ODBC 函数列表，而是指定支持的功能，如以下部分所列。 若要为某一功能提供支持，驱动程序必须支持对某些 ODBC 函数的部分或全部形式的调用 (有关详细信息，请参阅 [函数一致性](../../../odbc/reference/develop-app/function-conformance.md)) ，设置某些属性 (请参阅 [属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)) 和某些描述符字段 (参见 " [描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)) "。  
  
 应用程序通过连接到数据源并使用 SQL_ODBC_INTERFACE_CONFORMANCE 选项调用 **SQLGetInfo** 来发现驱动程序的接口一致性级别。  
  
 驱动程序可以自由地在其宣称完成一致性的级别之外实现功能。 应用程序通过调用 **SQLGetFunctions** (来确定存在的任何其他功能，以确定) 和 **SQLGetInfo** (查询各种 odbc 功能) 。  
  
 有三个 ODBC 接口一致性级别：核心、级别1和级别2。  
  
> [!NOTE]
>  这些一致性级别的要求不同于 ODBC 2.x 中具有相同名称的 ODBC API 一致性*级别。* 特别是，ODBC*2.X API 一致性* 级别1隐含的所有功能现在都属于核心接口一致性级别。 因此，许多 ODBC 驱动程序可能会报告核心级接口一致性。  
  
 本部分包含以下主题。  
  
-   [核心接口一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [级别 1 接口一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [级别 2 接口一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函数一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [属性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
