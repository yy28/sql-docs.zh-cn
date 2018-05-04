---
title: 垂直应用程序 |Microsoft 文档
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
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c89d0080f4cc29296d9e6dcd43911ee920af6683
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="vertical-applications"></a>垂直应用程序
垂直应用程序通常执行针对单个 DBMS 明确定义的任务。 例如，一个顺序输入应用程序跟踪在一家公司的订单。 这些类型的应用程序具有的共同点是通过应用程序开发人员通常设计数据库架构，并当应用程序可能会使用大量的不同 Dbms，它适用于单个 DBMS 单个客户。  
  
 因为垂直应用程序通常需要某些功能，如可滚动游标或事务，所以它们极少数情况下支持所有 Dbms。 相反，他们往往会将一组有限的 Dbms 之间高度可互操作。 通常情况下，垂直应用程序开发人员选择支持这些 Dbms，表示大量的市场而忽略其余副本。 他们甚至可以选择这些 Dbms 以减少其测试和产品支持成本支持特定的驱动程序。  
  
 由于垂直应用程序可以支持一组已知的 Dbms，它们有时包含特定于驱动程序或特定于 DBMS 的代码。 但是，在最低限度因为它需要额外的时间来维护最好保存此类代码。
