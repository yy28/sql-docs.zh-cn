---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc35f7bceff2d9e92b70448040bb602117b76c84
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47629635"
---
# <a name="dbms-based-drivers"></a>基于 DBMS 的驱动程序
基于 DBMS 的驱动程序用于如 Oracle 或 SQL Server 提供驱动程序使用一个独立的数据库引擎的数据源。 这些驱动程序通过独立引擎; 访问的物理数据即，它们提交到 SQL 语句，并从引擎中检索结果。  
  
 基于 DBMS 的驱动程序使用现有的数据库引擎，因为它们通常更轻松地编写比基于文件的驱动程序。 基于 DBMS 的驱动程序可以轻松实现将转换为本机 API 调用 ODBC 调用，尽管这会导致速度较慢的驱动程序。 实现基于 DBMS 的驱动程序的更好方法是使用基础数据流协议，这通常是本机 API 的定义。 例如，SQL Server 驱动程序应使用的 TDS （数据流协议适用于 SQL Server），而不是 DB 库 (用于 SQL Server 的本机 API)。 此规则的例外是 ODBC 时的本机 API。 例如，Watcom SQL 是一个独立的引擎，驻留在与应用程序在同一台计算机上，加载直接作为驱动程序。  
  
 基于 DBMS 的驱动程序充当客户端/服务器配置中的客户端数据源充当服务器的位置。 在大多数情况下，客户端 （驱动程序） 和服务器 （数据源） 位于不同的计算机，尽管两者可以驻留在同一台计算机运行的多任务操作系统上。 第三种可能性是*网关，* 这位于驱动程序和数据源之间。 网关是一种软件会导致一个 DBMS 与另一个类似的形式。 例如，编写使用 SQL Server 的应用程序还可以访问 DB2 数据通过 Micro Decisionware DB2 网关;此产品将导致 DB2 看起来像 SQL Server。  
  
 下图显示了三种不同配置的基于 DBMS 的驱动程序。 在第一个配置中，驱动程序和数据源位于同一台计算机上。 在第二个的驱动程序和数据源位于不同的计算机上。 在第三，驱动程序和数据源位于不同的计算机和网关位于之间它们驻留在另一个计算机上。  
  
 ![DBMS 的三种配置&#45;基于驱动程序](../../odbc/reference/media/pr07.gif "pr07")
