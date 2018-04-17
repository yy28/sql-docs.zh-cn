---
title: 基于 DBMS 的驱动程序 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9094b46014bad912dfa9f83de90cef0c25df1b9f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dbms-based-drivers"></a>基于 DBMS 的驱动程序
基于 DBMS 的驱动程序用于 Oracle 或 SQL Server 等的数据源提供要使用的驱动程序的独立数据库引擎。 这些驱动程序通过独立的引擎，则访问物理数据也就是说，它们提交到的 SQL 语句，并从引擎中检索结果。  
  
 由于基于 DBMS 的驱动程序使用现有的数据库引擎，它们是通常更轻松地编写上比基于文件的驱动程序。 虽然基于 DBMS 的驱动程序可以通过翻译对本机 API 调用的 ODBC 调用容易地实现，这会导致速度较慢的驱动程序。 更好的方法来实现基于 DBMS 的驱动程序是使用通常是本机 API 所执行的操作的基础数据流协议。 例如，SQL Server 驱动程序应使用的 TDS （数据流协议为 SQL Server），而不是 DB 库 (用于 SQL Server 的本机 API)。 此规则的例外是 ODBC 时的本机 API。 例如，Watcom SQL 是一个独立的引擎，驻留在与应用程序相同的计算机上，而且它直接为驱动程序加载。  
  
 基于 DBMS 的驱动程序充当客户端/服务器配置中的客户端数据源其中充当服务器。 大多数情况下，客户端 （驱动程序） 和服务器 （数据源） 驻留在不同计算机上虽然都无法位于同一台计算机运行多任务操作系统。 第三个可能是*网关，*其位于之间的驱动程序和数据源。 网关是一种软件导致如下所示另一个 DBMS。 例如，编写使用 SQL Server 的应用程序可以还访问 DB2 数据通过 Micro Decisionware DB2 网关;此产品将导致 DB2 为类似于 SQL Server。  
  
 下图显示三个不同配置的基于 DBMS 的驱动程序。 在第一个配置中，驱动程序和数据源位于同一台计算机上。 在第二个的驱动程序和数据源位于不同的计算机上。 在第三个、 驱动程序和数据源位于不同的计算机和网关位于之间它们位于另一个计算机上。  
  
 ![DBMS 的三种配置&#45;基于驱动程序](../../odbc/reference/media/pr07.gif "pr07")
