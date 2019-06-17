---
title: 选择网络协议 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 9c167994c7145bce348b6959a57533e398e1d6bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035276"
---
# <a name="choosing-a-network-protocol"></a>选择网络协议
  若要连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，必须启用网络协议。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以在同一时间服务上有多个协议的请求。 客户端用单个协议连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果客户端程序不知道 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在侦听哪个协议，可以配置客户端按顺序尝试多个协议。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器启用、禁用以及配置网络协议。  
  
## <a name="shared-memory"></a>Shared Memory  
 Shared Memory 是可供使用的最简单协议，没有可配置的设置。 由于使用 Shared Memory 协议的客户端仅可以连接到同一台计算机上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，因此它对于大多数数据库活动而言是没用的。 如果怀疑其他协议配置有误，请使用 Shared Memory 协议进行故障排除。  
  
> [!NOTE]  
>  使用 MDAC 2.8 或更早版本的客户端不能使用 Shared Memory 协议。 如果这些客户端尝试使用，将自动切换为 Named Pipes 协议。  
  
## <a name="tcpip"></a>TCP/IP  
 TCP/IP 是 Internet 上广泛使用的通用协议。 它与互连网络中硬件结构和操作系统各异的计算机进行通信。 TCP/IP 包括路由网络流量的标准，并能够提供高级安全功能。 它是目前在商业中最常用的协议。 将计算机配置为使用 TCP/IP 可能会很复杂，但大多数联网的计算机已经配置正确。 若要配置未在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中出现的 TCP/IP 设置，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文档。  
  
## <a name="named-pipes"></a>命名管道  
 Named Pipes 是为局域网而开发的协议。 内存的一部分被某个进程用来向另一个进程传递信息，因此一个进程的输出就是另一个进程的输入。 第二个进程可以是本地的（与第一个进程位于同一台计算机上），也可以是远程的（位于联网的计算机上）。  
  
## <a name="named-pipes-vs-tcpip-sockets"></a>Named Pipes 与TCP/IP 套接字  
 在快速局域网 (LAN) 环境中，传输控制协议或 Internet 协议 (TCP/IP) 套接字客户端和 Named Pipes 客户端在性能方面不相上下。 但是，网络速度越慢[如在广域网 (WAN) 或拨号网络上]，TCP/IP 套接字客户端与 Named Pipes 客户端的性能差异越明显。 这是因为进程间通信 (IPC) 的机制在对等项间的通信方式不同。  
  
 对于 Named Pipes，通常网络通信交互性更强。 一个对等方直到另一个对等方使用读取命令请求数据时才发送数据。 在开始读取数据前，网络读取一般包括一系列窥视 Named Pipes 的信息。 这在慢速网络中可能开销非常大，并会导致过多的网络流量，其他的网络客户端反过来也会受到影响。  
  
 阐明所讨论的是本地管道还是网络管道也很重要。 如果服务器应用程序在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机的本地运行，则可以选择本地 Named Pipes 协议。 本地 Named Pipes 以内核模式运行且速度非常快。  
  
 对于 TCP/IP 套接字，数据传输的效率更高，开销也更少。 数据传输还可以利用 TCP/IP 套接字性能增强机制的优点，例如窗口化、延迟确认等。 这在慢速网络中可能非常有益。 对于应用程序的不同类型，这类性能差异可能非常大。  
  
 TCP/IP 套接字还支持积压队列。 试图连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，与可能导致管道忙错误的 Named Pipes 相比，该队列可以带来有限的平稳效果。  
  
 通常，TCP/IP 在慢速 LAN、WAN 或拨号网络中效果较好。而当网络速度不成问题时，Named Pipes 则是更好的选择，因为其功能更强、更易于使用并具有更多的配置选项。  
  
## <a name="enabling-the-protocol"></a>启用协议  
 该协议必须在客户端和服务器上都启用才能正常工作。 服务器可以同时监听所有已启用的协议的请求。 客户端计算机可以选取一个协议，或按照 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中列出的顺序尝试这些协议。  
  
 有关如何配置协议和连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的简短教程，请参阅[教程：数据库引擎入门](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)。  
  
  
