---
title: 垂直应用 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc88f38fd1ffe8b2ee0033ad0a2abc4f15fd5cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300372"
---
# <a name="vertical-applications"></a>垂直应用程序
垂直应用程序通常针对单个 DBMS 执行定义良好的任务。 例如，订单输入应用程序跟踪公司中的订单。 这些类型的应用程序有共同之处是，数据库架构通常由应用程序开发人员设计，虽然应用程序可能使用许多不同的 DBMS，但它适用于单个客户的单个 DBMS。  
  
 由于垂直应用程序通常需要某些功能（如可滚动游标或事务），因此它们很少支持所有 DBMS。 相反，它们往往在有限的 DBMS 集中高度互操作。 通常，垂直应用程序开发人员选择支持那些代表市场很大一部分并忽略其余部分的 DBMS。 他们甚至可能选择支持这些 DBMS 的特定驱动程序，以降低其测试和产品支持成本。  
  
 由于垂直应用程序可以支持一组已知的 DBMS，因此它们有时包含特定于驱动程序或特定于 DBMS 的代码。 但是，最好将此类代码保持在最低限度，因为它需要额外的时间来维护。
