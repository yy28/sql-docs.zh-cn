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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5b9d731d12329a4ef663b1ea66cdc59a0b153fa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297975"
---
# <a name="transaction-support"></a>事务支持
对事务的支持程度由驱动程序定义。 ODBC 旨在在无需管理其数据的多个更新的单用户或桌面数据库上实现。 此外，某些支持事务的数据库仅为 SQL 的数据操作语言（DML）语句执行此操作;事务处于活动状态时，有关于使用数据定义语言（DDL）的限制或特殊事务语义。 也就是说，可能有事务支持对表进行多个同时更新，但不支持在事务中更改表的数目和定义。  
  
 应用程序通过使用 SQL_TXN_CAPABLE 选项调用**SQLGetInfo**来确定是否支持事务、是否可以在事务中包括 ddl 以及在事务中包括 ddl 的任何特殊影响。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。  
  
 如果驱动程序不支持事务，但应用程序可以（使用 ODBC 以外的 API）来锁定和解锁数据，则应用程序可以根据需要锁定和解锁记录和表来实现事务支持。 若要实现帐户传输示例，应用程序将锁定两个帐户的记录，复制当前值，借记第一个帐户，贷记第二个帐户，然后解锁记录。 如果任何步骤失败，应用程序将使用副本重置帐户。  
  
 即使是支持事务的数据源，也可能无法在特定环境中一次支持多个事务。 应用程序使用 SQL_MULTIPLE_ACTIVE_TXN 选项调用**SQLGetInfo** ，以确定数据源是否可以支持同一环境中的多个连接上的并发活动事务。 由于每个连接都有一个事务，因此仅对与同一数据源具有多个连接的应用程序才会出现这种情况。
