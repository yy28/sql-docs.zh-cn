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
manager: craigg
ms.openlocfilehash: df7a2d036692cefcd1b2ea2338d51938a11ea85a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208437"
---
# <a name="vertical-applications"></a>垂直应用程序
垂直应用程序通常执行针对单个 DBMS 明确定义的任务。 例如，订单输入应用程序跟踪在一家公司中的订单。 这些类型的应用程序具有的共同点是由应用程序开发人员通常设计数据库架构和，尽管应用程序可能适用于大量的不同 Dbms，它适用于与单个 DBMS 单个客户。  
  
 垂直应用程序通常需要某些功能，如可滚动游标或事务，因为它们很少支持所有的 Dbms。 相反，他们往往会在一组有限的 Dbms 之间高度可互操作。 通常情况下，垂直应用程序开发人员选择支持这些 Dbms 表示了相当一部分的市场和忽略其余部分。 他们甚至可以选择特定的驱动程序支持这些 Dbms，以减少其测试和产品支持成本。  
  
 由于垂直应用程序可以支持一组已知的 Dbms，它们有时包含特定于驱动程序或特定于 DBMS 的代码。 但是，在最低限度因为它需要额外的时间来维护最好保存此类代码。
