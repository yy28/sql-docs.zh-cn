---
description: 基于 DBMS 的驱动程序
title: 基于 DBMS 的驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 844c25ca32bdf302312df6d23ca8e1d85fe198c7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476909"
---
# <a name="dbms-based-drivers"></a>基于 DBMS 的驱动程序
基于 DBMS 的驱动程序与数据源（如 Oracle 或 SQL Server）一起使用，这些数据源提供独立的数据库引擎供驱动程序使用。 这些驱动程序通过独立引擎访问物理数据;也就是说，它们向引擎提交 SQL 语句并检索结果。  
  
 由于基于 DBMS 的驱动程序使用现有的数据库引擎，因此它们通常比基于文件的驱动程序更容易编写。 尽管可以通过将 ODBC 调用转换为本机 API 调用来轻松实现基于 DBMS 的驱动程序，但这会导致驱动程序速度变慢。 实现基于 DBMS 的驱动程序的更好方法是使用底层数据流协议，这通常是本机 API 的作用。 例如，SQL Server 驱动程序应使用 TDS (用于 SQL Server) 的数据流协议，而不是 (SQL Server 的本机 API 的 DB 库。 此规则的例外情况是 ODBC 是本机 API。 例如，Watcom SQL 是与应用程序驻留在同一台计算机上的独立引擎，并直接作为驱动程序加载。  
  
 基于 DBMS 的驱动程序在客户端/服务器配置中充当客户端，其中的数据源充当服务器。 在大多数情况下，客户端 (驱动程序) 和服务器 (数据源) 驻留在不同的计算机上，尽管两者都可以位于运行多任务操作系统的同一计算机上。 第三种可能性是位于驱动程序和数据源之间的 *网关* 。 网关是一种软件，它使一个 DBMS 看上去像另一个 DBMS。 例如，SQL Server 使用编写的应用程序还可以通过微 Decisionware DB2 网关访问 DB2 数据;此产品会使 DB2 看起来像 SQL Server。  
  
 下图显示了基于 DBMS 的驱动程序的三个不同配置。 在第一次配置中，驱动程序和数据源驻留在同一台计算机上。 在第二个版本中，驱动程序和数据源驻留在不同的计算机上。 在第三个版本中，驱动程序和数据源驻留在不同的计算机上，一个网关位于另一个计算机上。  
  
 ![基于 DBMS&#45;的驱动程序的三种配置](../../odbc/reference/media/pr07.gif "pr07")
