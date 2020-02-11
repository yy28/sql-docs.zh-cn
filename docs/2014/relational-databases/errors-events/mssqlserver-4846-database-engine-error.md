---
title: MSSQLSERVER_4846 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4846 (Database Engine error)
ms.assetid: a455e809-1883-4c7d-b3e3-835ee5bfe258
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b43cd194a2bfcf93b74b53fa2e9cb3a6a3eaff2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913787"
---
# <a name="mssqlserver_4846"></a>MSSQLSERVER_4846
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|4846|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|BULKPROV_MEMORY|  
|消息正文|大容量数据提供程序分配内存失败。|  
  
## <a name="explanation"></a>说明  
 内存分配失败。  
  
## <a name="user-action"></a>用户操作  
 执行以下一般步骤以解决内存错误：  
  
1.  验证其他应用程序或服务是否占用此服务器上的内存。 重新配置不太重要的应用程序或服务，使其占用更少的内存。  
  
2.  开始收集 **SQL Server: Buffer Manager**、**SQL Server: Memory Manager** 的性能监视器计数器。  
  
3.  检查以下 SQL Server 内存配置参数：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     注意任何不寻常的设置。 根据需要更正它们。 满足 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的内存要求。 SQL Server 联机丛书的“设置服务器配置选项”中列出了默认设置。  
  
4.  在您看到这些错误消息时，观察 DBCC MEMORYSTATUS 输出及其变化情况。  
  
5.  检查工作负荷（例如，并发会话数，当前执行的查询）。  
  
 以下操作可能会为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多内存：  
  
-   如果除 SQL Server 外的应用程序正在占用资源，请尝试停止运行这些应用程序，或者考虑在单独的服务器上运行它们。 这样做将消除外部内存压力。  
  
-   如果已配置 **max server memory**，请增大其设置。  
  
 运行以下 DBCC 命令以释放一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存缓存。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 如果问题仍存在，则您将需要进一步调查，可能需要减小工作负荷。  
  
  
