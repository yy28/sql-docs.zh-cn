---
title: "网络数据库访问 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 920de8b36ee55357eebde9ad844bfe569773f74e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="network-database-access"></a>网络数据库访问权限
通过网络访问数据库需要的许多组件，其中每个独立的并且位于下方的编程接口。 下图显示了这些组件。  
  
 ![要在网络访问的数据库组件](../../odbc/reference/media/pr04.gif "pr04")  
  
 每个组件的更多说明如下所示：  
  
-   **编程接口**编程接口如本节前面所述的包含所进行的应用程序调用。 这些接口 (embedded SQL，SQL 模块，并调用级接口) 是通常特定于每个 DBMS，尽管它们通常都基于 ANSI 或 ISO 标准。  
  
-   **数据流协议**数据流协议描述 DBMS 和其客户端之间传输数据的流。 例如，协议可能要求来描述流的其余部分包含的第一个字节： 要执行返回的错误值，或返回的数据的 SQL 语句。 然后，流中的数据的其余部分的格式都依赖于此标志。 例如，标志、 2 字节整数错误代码、 2 字节整数错误消息长度和一条错误消息可能包含错误流。  
  
     数据流协议是一种逻辑协议，并独立于基础网络使用的协议。 因此，通常可以在多种不同的网络上使用单个数据流协议。 数据流协议是通常专有的且具有对其进行了优化，若要使用特定 DBMS。  
  
-   **进程间通信机制**进程间通信 (IPC) 机制是依据一个进程与另一个进行通信的过程。 示例包括命名的管道、 TCP/IP 套接字和 DECnet 套接字。 IPC 机制的选择的操作系统和网络正在使用受约束。  
  
-   **网络协议**网络协议用于通过网络传输数据的流。 它可被视为联结支持用来实现数据的 IPC 机制流式传输协议，以及支持基本的网络操作，如文件传输和打印共享。 网络协议包括 NetBEUI、 TCP/IP、 DECnet 和 SPX/IPX 和特定于每个网络。
