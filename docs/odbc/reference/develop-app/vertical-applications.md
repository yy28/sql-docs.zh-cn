---
title: 垂直应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0ed7a5f488765b56b2af0688ca14361590ab44
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022097"
---
# <a name="vertical-applications"></a>垂直应用程序
垂直应用程序通常针对单个 DBMS 执行定义完善的任务。 例如，订单输入应用程序跟踪公司中的订单。 这种类型的应用程序通常是由应用程序开发人员设计的，而应用程序也可以使用多个不同的 Dbms，而该应用程序则适用于单个客户的单个 DBMS。  
  
 由于垂直应用程序通常需要某些功能（如可滚动游标或事务），因此它们很少支持所有 Dbms。 相反，它们往往在一组有限的 Dbms 之间具有高度可互操作性。 通常情况下，垂直应用程序开发人员选择支持代表一小部分市场并忽略剩余部分的 Dbms。 它们甚至可能会选择支持这些 Dbms 的特定驱动程序，以降低测试和产品支持成本。  
  
 由于垂直应用程序可以支持一组已知的 Dbms，因此它们有时包含特定于驱动程序的或特定于 DBMS 的代码。 不过，此类代码最好保持最小值，因为它需要额外的时间来维护。
