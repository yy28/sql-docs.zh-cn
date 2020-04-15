---
title: 网络数据库访问 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2237c725d6fe3696d1f28d80c09f22183f718de8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295580"
---
# <a name="network-database-access"></a>网络数据库访问权限
通过网络访问数据库需要许多组件，每个组件都独立于编程接口并位于编程接口下面。 下图显示了这些组件。  
  
 ![通过网络访问数据库的组件](../../odbc/reference/media/pr04.gif "pr04")  
  
 每个组件的进一步说明如下：  
  
-   **编程接口**如本节前面所述，编程接口包含应用程序发出的调用。 这些接口（嵌入式 SQL、SQL 模块和调用级接口）通常特定于每个 DBMS，尽管它们通常基于 ANSI 或 ISO 标准。  
  
-   **数据流协议**数据流协议描述在 DBMS 及其客户端之间传输的数据流。 例如，协议可能需要第一个字节来描述流的其余部分包含的内容：要执行的 SQL 语句、返回的错误值或返回的数据。 然后，流中其余数据的格式将依赖于此标志。 例如，错误流可能包含标志、2 字节整数错误代码、2 字节整数错误消息长度和错误消息。  
  
     数据流协议是一种逻辑协议，独立于基础网络使用的协议。 因此，单个数据流协议通常可以在多个不同的网络上使用。 数据流协议通常是专有的，并已经过优化以与特定的 DBMS 配合使用。  
  
-   **进程间通信机制**进程间通信 （IPC） 机制是一个进程与另一个进程通信的过程。 示例包括命名管道、TCP/IP 插槽和 DECnet 套接字。 IPC机制的选择受到操作系统和网络使用的限制。  
  
-   **网络协议**网络协议用于通过网络传输数据流。 它可以被视为支持用于实现数据流协议的 IPC 机制以及支持基本网络操作（如文件传输和打印共享）的管道。 网络协议包括 NetBEUI、TCP/IP、DECnet 和 SPX/IPX，并且特定于每个网络。
