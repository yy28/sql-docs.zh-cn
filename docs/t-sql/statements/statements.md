---
title: 语句 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: 7
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 07828132cb2413617b6b0d1141ae9a440e612559
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37790388"
---
# <a name="transact-sql-statements"></a>Transact-SQL 语句
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

本参考主题总结了用于 Transact-SQL (T-SQL) 的语句的类别。 左侧导航栏中列出了所有语句。

## <a name="backup-and-restore"></a>备份和还原
备份和还原语句提供创建备份和从备份中还原的方法。  有关详细信息，请参阅[备份和还原概述](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。

## <a name="data-definition-language"></a>数据定义语言
数据定义语言 (DDL) 语句定义数据结构。 使用以下语句在数据库中创建、更改或删除数据结构。
- ALTER
- 排序规则
- CREATE
- DROP
- DISABLE TRIGGER
- ENABLE TRIGGER
- RENAME
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>数据操作语言
数据操作语言 (DML) 影响存储在数据库中的信息。 使用以下语句在数据库中插入、更新和更改行。

- BULK INSERT
- 删除
- Insert
- UPDATE
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>权限语句
权限语句决定哪些用户和登录名可以访问数据并执行操作。 有关身份验证和访问权限的详细信息，请参阅[安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="service-broker-statements"></a>Service Broker 语句
Service Broker 是一项功能，可为消息和队列应用程序提供本机支持。 有关详细信息，请参阅 [Service Broker](../../relational-databases/service-broker/event-notifications.md)。

## <a name="session-settings"></a>会话设置
SET 语句决定当前会话处理运行时设置的方式。 如需查看概述，请参阅 [SET 语句](set-statements-transact-sql.md)。
