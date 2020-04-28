---
title: 其他驱动程序体系结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae047fe8014b806d3bda8b0513521b4ddda072a7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280527"
---
# <a name="other-driver-architectures"></a>其他驱动程序体系结构
某些 ODBC 驱动程序并不严格符合前面所述的体系结构。 这可能是因为驱动程序执行的任务不同于传统 ODBC 驱动程序的责任，或不是正常的驱动程序。  
  
## <a name="driver-as-a-middle-component"></a>驱动程序作为中间组件  
 ODBC 驱动程序可能位于驱动程序管理器与一个或多个其他 ODBC 驱动程序之间。 当中间的驱动程序能够处理多个数据源时，它将充当 ODBC 调用（或适当转换的调用）的调度程序，以访问实际访问数据源的其他模块。 在此体系结构中，中间的驱动程序正在考虑驱动程序管理器的某些角色。  
  
 此类驱动程序的另一个示例是针对 ODBC 的 spy 程序，它会截获和复制在驱动程序管理器和驱动程序之间发送的 ODBC 函数。 此层可用于模拟驱动程序或应用程序。 对于驱动程序管理器，该层显示为驱动程序;对于驱动程序，该层显示为驱动程序管理器。  
  
## <a name="heterogeneous-join-engines"></a>异类联接引擎  
 某些 ODBC 驱动程序是基于用于执行异类联接的查询引擎构建的。 在一个异类联接引擎的体系结构中（请参阅下图），驱动程序作为驱动程序出现在应用程序中，但作为应用程序显示给驱动程序管理器的另一个实例。 此驱动程序通过在每个已联接数据库的驱动程序中调用单独的 SQL 语句来处理应用程序中的异类联接。  
  
 ![异类联接引擎的体系结构](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 此体系结构为应用程序提供了一个公共接口，用于访问不同数据库中的数据。 它可以使用一种常用的方法来检索元数据，例如有关特殊列（行标识符）的信息，并且它可以调用常见目录函数来检索数据字典信息。 例如，通过调用 ODBC 函数**SQLStatistics**，应用程序可以检索有关要联接的表的索引的信息，即使这些表位于两个不同的数据库中。 查询处理器不必担心数据库存储元数据的方式。  
  
 应用程序还对数据类型具有标准访问权限。 ODBC 定义将特定于 DBMS 的数据类型映射到的常见 SQL 数据类型。 应用程序可以调用**SQLGetTypeInfo**来检索有关不同数据库上的数据类型的信息。  
  
 当应用程序生成异类联接语句时，此体系结构中的查询处理器会分析 SQL 语句，然后为要联接的每个数据库生成独立的 SQL 语句。 通过使用有关每个驱动程序的元数据，查询处理器可以确定最高效的智能联接。 例如，如果语句将一个数据库中的两个表与另一个数据库中的一个表联接，则查询处理器可以在将结果与其他数据库中的表联接之前，联接其中的两个表。  
  
## <a name="odbc-on-the-server"></a>服务器上的 ODBC  
 ODBC 驱动程序可以安装在服务器上，以便应用程序可以在一系列客户端计算机上的任何一台计算机上使用它们。 在此体系结构中（请参阅下图），驱动程序管理器和单个 ODBC 驱动程序安装在每个客户端上，另一个驱动程序管理器和一系列 ODBC 驱动程序安装在服务器上。 这样，每个客户端都可以访问服务器上使用和维护的各种驱动程序。  
  
 ![服务器上的 ODBC 驱动程序的体系结构](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 此体系结构的一个优点是高效的软件维护和配置。 驱动程序只需在一个位置进行更新：在服务器上。 通过使用系统数据源，可以在服务器上定义数据源，供所有客户端使用。 不需要在客户端上定义数据源。 连接池可用于简化客户端连接到数据源的过程。  
  
 客户端上的驱动程序通常是一个非常小的驱动程序，用于将驱动程序管理器调用传输到服务器。 其占用量明显小于服务器上的功能齐全的 ODBC 驱动程序。 在此体系结构中，如果服务器具有更多的计算能力，则可以释放客户端资源。 此外，通过安装备份服务器并执行负载平衡来优化服务器使用，可以增强整个系统的效率和安全性。
