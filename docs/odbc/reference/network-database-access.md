---
title: 网络数据库访问权限 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f8eaebca02ef3987e3613b5dd896e0f7c130086
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938036"
---
# <a name="network-database-access"></a>网络数据库访问权限
在网络上访问数据库需要多个组件，其中每个独立的并且位于下方的编程接口。 下图显示了这些组件。  
  
 ![组件跨网络访问的数据库](../../odbc/reference/media/pr04.gif "pr04")  
  
 每个组件的进一步说明如下所示：  
  
-   **编程接口**编程接口如前文所述在本部分中，包含由应用程序进行的调用。 这些接口 (嵌入式 SQL，SQL 模块，以及如何调用级别接口) 是通常特定于每个 DBMS，尽管它们通常都基于 ANSI 或 ISO 标准。  
  
-   **数据 Stream 协议**数据流协议描述 DBMS 和其客户端之间传输数据的流。 例如，协议可能要求来描述流的其余部分包含的第一个字节： 执行返回的错误值，或返回数据的 SQL 语句。 然后，流中的数据的其余部分的格式将取决于此标志。 例如，标志、 2 字节整数错误代码、 2 字节整数错误消息长度和一条错误消息可能包含错误流。  
  
     数据流协议是一种逻辑协议，并独立于基础网络使用的协议。 因此，通常可以在多种不同的网络上使用单个数据流协议。 数据流协议是通常专用和已经过优化，以使用特定 DBMS。  
  
-   **进程间通信机制**进程间通信 (IPC) 机制是依据一个流程与另一个进行通信的过程。 示例包括命名的管道、 TCP/IP 套接字和 DECnet 套接字。 所选的 IPC 机制受操作系统和所使用的网络。  
  
-   **网络协议**网络协议用于通过网络传输的数据流。 它可被视为支持用于实现数据的 IPC 机制流式传输协议，以及支持基本的网络操作，如文件传输和打印共享的基本功能。 网络协议包括 NetBEUI、 TCP/IP、 DECnet 和 SPX/IPX 和特定于每个网络。
