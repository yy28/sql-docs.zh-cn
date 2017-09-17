---
title: "其他驱动程序体系结构 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a458ba0d7e83ab4e4c56ed40c34fae54e24c1b2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="other-driver-architectures"></a>其他驱动程序体系结构
某些 ODBC 驱动程序严格不符合前面所述的体系结构。 这可能是因为驱动程序履行之外的传统的 ODBC 驱动程序，或不是在正常的意义上的驱动程序。  
  
## <a name="driver-as-a-middle-component"></a>驱动程序作为中间组件  
 ODBC 驱动程序可以驻留之间驱动程序管理器和一个或多个其他 ODBC 驱动程序。 能够处理多个数据源中中间的驱动程序时，它充当调度程序的实际访问的数据源的其他模块 ODBC 调用 （或相应地已翻译的调用）。 在此体系结构，在中间的驱动程序要对其执行某些角色的驱动程序管理器。  
  
 这种驱动程序的另一个示例是 spy 程序适用于 ODBC，这会截获，并将复制 ODBC 驱动程序管理器和驱动程序之间发送的函数。 此层可以用于模拟驱动程序或应用程序。 到驱动程序管理器中，层似乎是驱动程序;到驱动程序，层看起来驱动程序管理器。  
  
## <a name="heterogeneous-join-engines"></a>异类联接引擎  
 为执行异类联接的查询引擎为基础构建某些 ODBC 驱动程序。 在一个体系结构中的异类联接引擎 （参见下图），该驱动程序将显示应用程序为驱动程序而是显示在到另一实例的驱动程序管理器中为应用程序。 此驱动程序处理从应用程序的异类联接，通过调用驱动程序中的单独的 SQL 语句，为每个已联接的数据库。  
  
 ![体系结构的异类联接引擎](../../odbc/reference/media/fig3-4.gif "fig3 4")  
  
 此体系结构提供一个通用界面执行应用程序从不同的数据库访问数据。 它可以使用检索元数据，例如特殊列 （行标识符） 的信息的常用方法，以及它可调用公共目录函数来检索数据字典信息。 通过调用 ODBC 函数**SQLStatistics**，例如，应用程序可以检索要联接的表有关的索引信息，即使表位于两个单独的数据库。 查询处理器不必担心如何数据库存储元数据。  
  
 应用程序还具有标准访问权限，为数据类型。 ODBC 定义特定于 DBMS 的数据类型映射到的常见 SQL 数据类型。 应用程序可以调用**SQLGetTypeInfo**检索有关数据类型不同的数据库的信息。  
  
 当应用程序生成异类联接语句时，此体系结构中的查询处理器将分析 SQL 语句，，然后生成单独的 SQL 语句为每个要联接的数据库。 通过使用有关每个驱动程序的元数据，查询处理器可以确定最高效、 智能联接。 例如，如果该语句对另一个数据库上的一个表的一个数据库连接两个表，查询处理器可以将联接两个表上一个数据库联接结果与其他数据库中的表之前。  
  
## <a name="odbc-on-the-server"></a>在服务器上的 ODBC  
 可以在服务器上安装 ODBC 驱动程序，以便在任何一系列的客户端计算机上的应用程序都可以使用它们。 此体系结构中 （请参阅下图），在每个客户端上安装驱动程序管理器和单独的 ODBC 驱动程序和服务器上安装另一个驱动程序管理器和一系列的 ODBC 驱动程序。 这允许各种驱动程序使用并且在服务器上维护每个客户端访问。  
  
 ![在服务器上的 ODBC 驱动程序的体系结构](../../odbc/reference/media/fig3-5.gif "FIG3 5")  
  
 此体系结构的优势之一是有效地进行软件维护和配置。 驱动程序需要仅在一个位置更新： 在服务器上。 通过使用系统数据源，数据源可以使用的服务器上定义的所有客户端。 不需要客户端上定义的数据源。 可以使用连接池来简化依据客户端连接到数据源的过程。  
  
 客户端上的驱动程序通常是非常小的驱动程序传输到服务器的驱动程序管理器调用。 其占用量可以显著小于服务器上完全正常运行的 ODBC 驱动程序。 在此体系结构，如果服务器有更多计算能力可以释放客户端资源。 此外，可以通过安装备份服务器并执行负载平衡来优化服务器，请使用增强的效率和安全性整个系统。
