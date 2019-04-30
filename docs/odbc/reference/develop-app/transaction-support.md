---
title: 事务支持 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be133079c1b6beffd484942eb9ae058c14dd5c1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306039"
---
# <a name="transaction-support"></a>事务支持
对事务程度是支持的驱动程序定义的。 ODBC 被设计为具有无需管理其数据的多个更新的单用户或桌面数据库上实现。 此外，某些支持事务的数据库执行操作因此仅限于 SQL、 数据操作语言 (DML) 语句限制或特殊事务语义与使用数据定义语言 (DDL) 时有一个事务处于活动状态。 也就是说，可能存在有关表的多个同时进行更新而不是更改的数量和事务处理期间的表定义的事务支持。  
  
 应用程序确定是否支持事务，是否可以在一个事务，并通过调用在事务中，包括 DDL 的任何特殊效果包含 DDL **SQLGetInfo** SQL_TXN_CAPABLE 选项。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。  
  
 如果该驱动程序不支持事务，但应用程序必须 （使用 ODBC 以外的 API） 的功能锁定和解锁数据，应用程序可以实现锁定和解锁的记录和根据需要的表的事务支持。 若要实现帐户转移示例，应用程序将锁定的记录这两个帐户、 复制当前值、 第一个帐户中借记、 信用额度的第二个帐户，和解除锁定记录。 如果任何步骤失败，应用程序会重置的帐户使用这些副本。  
  
 支持事务的甚至数据源可能不能以支持多个事务在特定环境中一次。 应用程序调用**SQLGetInfo** SQL_MULTIPLE_ACTIVE_TXN 选项以确定数据源是否可以在同一环境中的多个连接上支持同时进行的活动事务。 由于每个连接的一个事务，这是仅有相同的数据源的多个连接的应用程序感兴趣。
