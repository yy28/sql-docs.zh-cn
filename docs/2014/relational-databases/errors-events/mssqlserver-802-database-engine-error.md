---
title: MSSQLSERVER_802 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 802 (Database Engine error)
ms.assetid: 5892ed24-4dcb-4bf9-a8a4-a7ca898832d5
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bd0ed39287cd9f4a61888aba817821f0ef16e584
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129886"
---
# <a name="mssqlserver802"></a>MSSQLSERVER_802
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|802|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NO_BUFS|  
|消息正文|缓冲池中的可用内存不足。|  
  
## <a name="explanation"></a>解释  
 当缓冲池已满且缓冲池无法再增大时，会导致此错误。  
  
## <a name="user-action"></a>用户操作  
 下面的列表概述了有助于解决内存错误的一般步骤：  
  
1.  验证其他应用程序或服务是否占用此服务器上的内存。 重新配置不太重要的应用程序或服务，使其占用更少的内存。  
  
2.  开始收集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Buffer Manager**、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Memory Manager** 的性能监视器计数器。  
  
3.  检查下面的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存配置参数：  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
     注意任何不寻常的设置，并根据需要更正它们。 满足 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更高内存要求。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书的“设置服务器配置选项”中列出了默认设置。  
  
4.  在您看到这些错误消息时，观察 DBCC MEMORYSTATUS 输出及其变化情况。  
  
5.  检查工作负荷（并发会话数、当前执行的查询）。  
  
 以下操作可能会为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更多内存：  
  
-   如果除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外的应用程序正在占用资源，请尝试停止这些应用程序，或者在单独的服务器上运行它们。  
  
-   如果已配置 **max server memory**，请增大该设置。  
  
 运行以下 DBCC 命令以释放一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存缓存。  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
 如果问题仍存在，则您将需要进一步调查，可能需要减小工作负荷。  
  
  