---
title: "语句 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d780aa463f6d4defe7dc727091863feabe7f338a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="transact-sql-statements"></a>Transact-SQL 语句
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

本参考主题总结了用于 TRANSACT-SQL (T-SQL) 语句的类别。 你可以找到所有左侧的导航栏中列出的语句。

## <a name="backup-and-restore"></a>备份和还原
备份和还原语句提供方法创建备份和从备份中还原。  有关详细信息，请参阅[备份和还原概述](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。

## <a name="data-definition-language"></a>数据定义语言
数据定义语言 (DDL) 语句定义数据结构。 这些语句用于创建、 更改或删除数据库中的数据结构。
- ALTER
- 排序规则
- CREATE
- DROP
- 禁用触发器
- ENABLE TRIGGER
- 重命名
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>数据操作语言
数据操作语言 (DML) 会影响存储在数据库中的信息。 这些语句用于插入、 更新和更改数据库中的行。

- BULK INSERT
- DELETE
- Insert
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>权限语句
权限语句确定哪些用户和登录名可以访问数据并执行操作。 有关身份验证和访问的详细信息，请参阅[安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="service-broker-statements"></a>Service Broker 语句
Service Broker 已为消息和队列的应用程序提供本机支持的功能。 有关详细信息，请参阅[Service Broker](../../relational-databases/service-broker/event-notifications.md)。

## <a name="session-settings"></a>会话设置
SET 语句确定当前的会话句柄运行时间设置的方式。 有关概述，请参阅[SET 语句](set-statements-transact-sql.md)。

