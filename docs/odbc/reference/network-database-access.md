---
description: 网络数据库访问权限
title: 网络数据库访问 |Microsoft Docs
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
ms.openlocfilehash: 025959072b7ebadc96fd1d1a628bdfaf5d449940
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461319"
---
# <a name="network-database-access"></a>网络数据库访问权限
跨网络访问数据库需要多个组件，其中每个组件都独立于并且位于编程接口的下面。 下图显示了这些组件。  
  
 ![通过网络访问数据库的组件](../../odbc/reference/media/pr04.gif "pr04")  
  
 后面的每个组件的详细说明如下：  
  
-   **编程接口** 如本部分前面所述，编程接口包含应用程序发出的调用。 这些接口 (嵌入的 SQL、SQL 模块和调用级接口) 通常特定于每个 DBMS，尽管它们通常基于 ANSI 或 ISO 标准。  
  
-   数据流**协议**数据流协议描述 DBMS 与其客户端之间传输的数据流。 例如，该协议可能需要第一个字节来描述流的其余部分所包含的内容：要执行的 SQL 语句、返回的错误值或返回的数据。 流中数据的其余部分的格式将取决于此标志。 例如，错误流可能包含标志、2字节整数错误代码、2字节整数错误消息长度和错误消息。  
  
     数据流协议是一种逻辑协议，与基础网络使用的协议无关。 因此，单个数据流协议通常可用于多个不同的网络。 数据流协议通常是专有的，已进行了优化，可与特定 DBMS 一起使用。  
  
-   **进程间通信机制** (IPC) 机制的进程间通信是指一个进程与另一个进程进行通信的过程。 示例包括命名管道、TCP/IP 套接字和 DECnet 套接字。 选择 IPC 机制受使用的操作系统和网络约束。  
  
-   **网络协议** 网络协议用于通过网络传输数据流。 它可以被视为支持用于实现数据流协议的 IPC 机制的管道，并支持基本的网络操作，如文件传输和打印共享。 网络协议包括 NetBEUI、TCP/IP、DECnet 和 SPX/IPX，并特定于每个网络。
