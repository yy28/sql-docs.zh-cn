---
title: "服务器属性（“内存”页）| Microsoft Docs"
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.serverproperties.memory.f1
ms.assetid: 46a77d4e-ab92-49d3-a14b-423462e50715
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b9ae03362f1dfb89aaebc09aabfed60c327a9d3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="server-properties---memory-page"></a>服务器属性 -“内存”页
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用此页可以查看或修改服务器内存选项。 当 **“最小服务器内存”** 设置为 0 而 **“最大服务器内存”** 设置为 2147483647 MB 时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以在任何给定的时间使用最合理的内存量，具体取决于操作系统以及其他应用程序当前使用的内存量。 当计算机和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的负载更改时，分配的内存也会更改。 可以进一步将此动态内存分配限制为下面指定的最小值和最大值。  
  
## <a name="options"></a>选项  
 **最小服务器内存(MB)**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应该至少以分配的最小内存量启动，在低于此值时不释放内存。 请根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的大小和活动设置此值。 始终将此选项设置为合理的值，以确保操作系统不会从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 请求过多的内存，从而避免降低 Windows 的性能。  
  
 **最大服务器内存(MB)**  
 指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动和运行时它可以分配的内存最大量。 如果知道有多个应用程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同时运行，并且要保证这些应用程序有足够的内存运行，则可以将此配置选项设置为特定值。 如果这些应用程序（如 Web 服务器或电子邮件服务器）只是按需请求内存，则不必设置该选项，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将会根据需要向它们释放内存。 但是，应用程序通常在启动时使用全部可用内存，并且也不会根据需要请求更多内存。 如果以这种方式运行的应用程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同时运行在同一台计算机上，则请设置该选项的值，保证应用程序所需的内存不会由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]来分配。 可以为 **max server memory** 指定的最小内存量为 128 MB。 （可为较旧的 32 位系统指定 64 兆字节 (MB)。）  
  
 **创建索引占用的内存(KB，0 = 动态内存)**  
 指定在索引创建排序过程中要使用的内存量 (KB)。 默认值为零，表示启用动态分配，在大多数情况下，无需进一步调整即可正常工作；不过，用户可以输入 704 到 2147483647 之间的其他值。  
  
> [!NOTE]  
>  不允许使用 1 到 703 之间的值。 如果输入此范围的值，该字段将使用 704 覆盖所输入的值。  
  
 **每次查询占用的最小内存(KB)**  
 指定为执行查询分配的内存量 (KB)。 用户可以将值从 512 设置为 2147483647 KB。 默认值为 1024 KB。  
  
 **配置值**  
 显示此窗格上选项的配置值。 如果更改了这些值，请单击 **“运行值”** 以查看更改是否已生效。 如果尚未生效，则必须首先重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 **“运行值”**  
 显示此窗格上选项的当前运行值。 这些值是只读的。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
