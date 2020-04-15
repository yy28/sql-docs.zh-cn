---
title: 基于 DBMS 的驱动程序 |微软文档
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
ms.openlocfilehash: 4e7b7b153d0b0cb0a3e6a3d738908b0039b95679
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306483"
---
# <a name="dbms-based-drivers"></a>基于 DBMS 的驱动程序
基于 DBMS 的驱动程序与数据源（如 Oracle 或 SQL Server）一起使用，这些数据源提供独立数据库引擎供驱动程序使用。 这些驱动程序通过独立引擎访问物理数据;也就是说，它们向引擎提交 SQL 语句并从引擎中检索结果。  
  
 由于基于 DBMS 的驱动程序使用现有的数据库引擎，因此它们通常比基于文件的驱动程序更易于写入。 尽管通过将 ODBC 调用转换为本机 API 调用可以轻松实现基于 DBMS 的驱动程序，但这将导致驱动程序变慢。 实现基于 DBMS 的驱动程序的更好方法是使用基础数据流协议，这通常是本机 API 的作用。 例如，SQL Server 驱动程序应使用 TDS（SQL Server 的数据流协议），而不是数据库库（SQL Server 的本机 API）。 此规则的一个例外是当 ODBC 是本机 API 时。 例如，Watcom SQL 是一个独立的引擎，它驻留在与应用程序相同的计算机上，并且直接作为驱动程序加载。  
  
 基于 DBMS 的驱动程序充当客户端/服务器配置中的客户端，数据源在其中充当服务器。 在大多数情况下，客户端（驱动程序）和服务器（数据源）驻留在不同的计算机上，尽管两者可以驻留在运行多任务操作系统的同一台计算机上。 第三种可能性是*网关，* 它位于驱动程序和数据源之间。 网关是使一个 DBMS 看起来像另一个软件。 例如，编写用于 SQL Server 的应用程序还可以通过微决策软件 DB2 网关访问 DB2 数据;此产品使 DB2 看起来像 SQL 服务器。  
  
 下图显示了基于 DBMS 的驱动程序的三种不同配置。 在第一个配置中，驱动程序和数据源驻留在同一台计算机上。 在第二个中，驱动程序和数据源驻留在不同的计算机上。 在第三个中，驱动程序和数据源驻留在不同的计算机上，网关位于它们之间，驻留在另一台计算机上。  
  
 ![基于 DBMS&#45;驱动程序的三种配置](../../odbc/reference/media/pr07.gif "pr07")
