---
title: 其他驱动程序体系结构 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280527"
---
# <a name="other-driver-architectures"></a>其他驱动程序体系结构
某些 ODBC 驱动程序与前面描述的体系结构不完全一致。 这可能是因为驱动程序执行传统 ODBC 驱动程序以外的职责，或者不是正常意义上的驱动程序。  
  
## <a name="driver-as-a-middle-component"></a>驱动程序作为中间组件  
 ODBC 驱动程序可能位于驱动程序管理器和一个或多个其他 ODBC 驱动程序之间。 当中间的驱动程序能够处理多个数据源时，它将充当 ODBC 调用（或适当转换的呼叫）到实际访问数据源的其他模块的调度程序。 在此体系结构中，中间的驱动程序承担了驱动程序管理器的一些角色。  
  
 此类驱动程序的另一个示例是 ODBC 的间谍程序，它拦截和复制在驱动程序管理器和驱动程序之间发送的 ODBC 函数。 此层可用于模拟驱动程序或应用程序。 对驱动程序管理器，图层似乎是驱动程序;对驱动程序，则图层显示为驱动程序。对驱动程序，图层显示为驱动程序管理器。  
  
## <a name="heterogeneous-join-engines"></a>异构连接引擎  
 某些 ODBC 驱动程序基于用于执行异构联接的查询引擎构建。 在异构联接引擎的一个体系结构中（请参阅下图），驱动程序在应用程序中显示为驱动程序，但在驱动程序管理器的另一个实例中显示为应用程序。 此驱动程序通过在每个联接数据库的驱动程序中调用单独的 SQL 语句来处理来自应用程序的异构联接。  
  
 ![异类联接引擎的体系结构](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 此体系结构为应用程序提供了一个通用接口，用于从不同的数据库访问数据。 它可以使用一种常用方法来检索元数据，例如有关特殊列（行标识符）的信息，并且它可以调用通用目录函数来检索数据字典信息。 例如，通过调用 ODBC 函数**SQLStatistics，** 应用程序可以检索有关要联接的表上的索引的信息，即使表位于两个单独的数据库中也是如此。 查询处理器不必担心数据库如何存储元数据。  
  
 该应用程序还可以对数据类型进行标准访问。 ODBC 定义特定于 DBMS 的数据类型映射到的常见 SQL 数据类型。 应用程序可以调用**SQLGetTypeInfo**来检索有关不同数据库中数据类型的信息。  
  
 当应用程序生成异构联接语句时，此体系结构中的查询处理器解析 SQL 语句，然后为每个要联接的数据库生成单独的 SQL 语句。 通过使用有关每个驱动程序的元数据，查询处理器可以确定最高效、最智能的联接。 例如，如果语句将一个数据库上的两个表与另一个数据库上的一个表联接，则查询处理器可以在将结果与另一个数据库的表联接之前将一个数据库上的两个表联接在一起。  
  
## <a name="odbc-on-the-server"></a>服务器上的 ODBC  
 ODBC 驱动程序可以安装在服务器上，以便应用程序可以在一系列客户端计算机上使用它们。 在此体系结构中（请参见下图），每个客户端上都安装了驱动程序管理器和单个 ODBC 驱动程序，并在服务器上安装了另一个驱动程序管理器和一系列 ODBC 驱动程序。 这允许每个客户端访问服务器上使用和维护的各种驱动程序。  
  
 ![服务器上的 ODBC 驱动程序的体系结构](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 此体系结构的一个优点是高效的软件维护和配置。 驱动程序只需在一个位置更新：在服务器上。 通过使用系统数据源，可以在服务器上定义数据源，供所有客户端使用。 不需要在客户端上定义数据源。 连接池可用于简化客户端连接到数据源的过程。  
  
 客户端上的驱动程序通常是将驱动程序管理器调用传输到服务器的非常小的驱动程序。 其占用空间可以比服务器上功能齐全的 ODBC 驱动程序小得多。 在此体系结构中，如果服务器具有更大的计算能力，则可以释放客户端资源。 此外，通过安装备份服务器和执行负载平衡来优化服务器使用，可以增强整个系统的效率和安全性。
