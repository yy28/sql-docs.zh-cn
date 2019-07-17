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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dbfb09a261d7499e07137b7ed830d5a5b92dc73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086012"
---
# <a name="other-driver-architectures"></a>其他驱动程序体系结构
某些 ODBC 驱动程序不严格符合到前面所述的体系结构。 这可能是因为驱动程序执行任务，而非传统的 ODBC 驱动程序，或不是通常意义上的驱动程序。  
  
## <a name="driver-as-a-middle-component"></a>驱动程序，因为中间组件  
 ODBC 驱动程序可能位于驱动程序管理器和一个或多个其他 ODBC 驱动程序之间。 支持使用多个数据源的中间驱动程序时，它充当调度程序的 ODBC 调用 （或相应地翻译后的调用） 与实际访问的数据源的其他模块。 在此体系结构，在中间的驱动程序要对其执行某些角色的驱动程序管理器。  
  
 这种驱动程序的另一个示例是 ODBC，这会截获并将驱动程序管理器和驱动程序之间发送的 ODBC 函数复制的监视程序。 此层可用于模拟驱动程序或应用程序。 为驱动程序管理器中，层似乎是驱动程序;该驱动程序，该图层似乎是驱动程序管理器。  
  
## <a name="heterogeneous-join-engines"></a>异类联接引擎  
 某些 ODBC 驱动程序用于执行异类联接的查询引擎为基础构建。 异类联接引擎的一个体系结构中 （请参阅下图），驱动程序将显示到应用程序，如驱动程序而是显示为另一个实例的驱动程序管理器应用程序。 此驱动程序通过为每个联接的数据库驱动程序中调用单独的 SQL 语句处理异类联接从应用程序。  
  
 ![异类联接引擎的体系结构](../../odbc/reference/media/fig3-4.gif "fig3 4")  
  
 此体系结构提供从不同的数据库访问数据的应用程序的常见界面。 它可以使用的常用方法来检索元数据，例如特殊列 （行标识符） 的信息，并且可以调用公共目录函数来检索数据字典信息。 通过调用 ODBC 函数**SQLStatistics**，例如，应用程序中检索信息有关的索引表进行联接，即使表在两个独立数据库。 查询处理器不必担心如何存储元数据数据库。  
  
 应用程序还具有标准访问的数据类型。 ODBC 定义特定于 DBMS 的数据类型映射到的公共 SQL 数据类型。 应用程序可以调用**SQLGetTypeInfo**来检索有关数据类型在不同的数据库的信息。  
  
 当应用程序生成异类联接语句时，此体系结构中的查询处理器将分析 SQL 语句，然后生成单独的 SQL 语句为每个要联接的数据库。 通过使用每个驱动程序有关的元数据，查询处理器可以确定最高效、 智能联接。 例如，如果该语句与另一个数据库上的一个表的一个数据库上联接两个表，查询处理器可以加入两个表上的一个数据库加入与其他数据库中的表结果之前。  
  
## <a name="odbc-on-the-server"></a>在服务器上的 ODBC  
 可以在服务器上安装 ODBC 驱动程序，以便可以在任何一系列的客户端计算机上的应用程序使用它们。 在此体系结构 （请参阅下图），驱动程序管理器和单个 ODBC 驱动程序安装在每个客户端和服务器上安装另一个驱动程序管理器和一系列的 ODBC 驱动程序。 这允许使用和服务器上维护的驱动程序的各种每个客户端访问。  
  
 ![在服务器上的 ODBC 驱动程序的体系结构](../../odbc/reference/media/fig3-5.gif "FIG3 5")  
  
 此体系结构的一个优点是高效的软件维护和配置。 只需在一个位置更新驱动程序： 在服务器上。 通过使用系统数据源，数据源可以使用在服务器上定义的所有客户端。 不需要在客户端上定义的数据源。 可以使用连接池来简化的客户端连接到数据源的过程。  
  
 客户端上的驱动程序通常是一个非常小的驱动程序，以便将传输到服务器的驱动程序管理器调用。 其占用量可以远远小于服务器上完全正常运行的 ODBC 驱动程序。 在此体系结构，如果服务器具有更多计算能力可以释放客户端资源。 此外，可以通过安装备份服务器并执行负载平衡来优化服务器，请使用增强的效率和整个系统的安全性。
