---
title: 交易支持 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5b9d731d12329a4ef663b1ea66cdc59a0b153fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297975"
---
# <a name="transaction-support"></a>事务支持
对事务的支持程度是驱动程序定义的。 ODBC 设计为在单用户或桌面数据库上实现，无需管理其数据的多个更新。 此外，某些支持事务的数据库仅针对 SQL 的数据操作语言 （DML） 语句执行此操作;当事务处于活动状态时，有关数据定义语言 （DDL） 的使用存在限制或特殊事务语义。 也就是说，对于表的多个同时更新，可能存在事务支持，但对于在事务期间更改表的数量和定义，则不支持事务支持。  
  
 应用程序通过使用 SQL_TXN_CAPABLE 选项调用**SQLGetInfo，** 确定是否支持事务、是否可以将 DDL 包含在事务中以及将 DDL 包含在事务中的任何特殊效果。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。  
  
 如果驱动程序不支持事务，但应用程序能够（使用 ODBC 以外的 API）锁定和解锁数据，则应用程序可以通过根据需要锁定和解锁记录和表来实现事务支持。 要实现帐户转移示例，应用程序将锁定两个帐户的记录、复制当前值、借记第一个帐户、贷记第二个帐户以及解锁记录。 如果任何步骤失败，应用程序将使用副本重置帐户。  
  
 即使支持事务的数据源也可能无法在特定环境中一次支持多个事务。 应用程序使用SQL_MULTIPLE_ACTIVE_TXN选项调用**SQLGetInfo，** 以确定数据源是否可以支持同一环境中多个连接上同时处于活动状态事务。 由于每个连接都有一个事务，因此对于与同一数据源具有多个连接的应用程序仅感兴趣。
