---
title: 其他复制升级问题 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system tables [SQL Server], replication
- passwords [SQL Server replication]
- versions [SQL Server replication]
- connections [SQL Server replication]
- scripts [SQL Server replication]
- ActiveX controls [SQL Server replication]
ms.assetid: 8a5e74be-4992-4f17-b20c-c3dce8f49329
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dd8ae8bb1080d92bb6a4ad1ba982f1dffc6d51f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093636"
---
# <a name="other-replication-upgrade-issues"></a>其他复制升级问题
  本主题涵盖了许多未由升级顾问报告的升级问题。  
  
## <a name="versions-supported"></a>支持的版本  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级复制的数据库。 在升级某个节点时，不必停止其他节点的活动。 请务必遵守有关拓扑中支持哪些版本的规则。  
  
 当你复制之间或不同版本间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，通常限于正在使用的最早版本的功能。  
  
> [!NOTE]  
>  由于 64 位和 32 位环境中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘存储格式相同，因此复制拓扑可以将运行于 32 位环境中的服务器实例与运行于 64 位环境中的服务器实例结合起来。  
  
 对于所有类型的复制，分发服务器版本不得低于发布服务器版本。 （分发服务器通常与发布服务器是同一个实例。）  
  
 对于事务复制，用于事务发布的订阅服务器版本可以是两个发布服务器版本中的任何一个版本。  
  
 对于合并复制，用于合并发布的订阅服务器的版本不能比发布服务器版本高。  
  
## <a name="merge-replication-batches-changes"></a>对合并复制批次进行的更改  
 为提高性能，合并代理执行的更改是成批执行的；因此，可以在一个语句内插入、更新或删除多行。 如果发布数据库或订阅数据库中任何已发布的表都有触发器，请确保这些触发器可以处理插入、更新和删除多行的操作。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“DML 触发器的多行注意事项”。  
  
## <a name="activex-control-changes"></a>对 ActiveX 控件进行的更改  
 已经针对复制 ActiveX 控件进行了如下更改：  
  
-   所有 ActiveX 控件都标记为对脚本编写和初始化不安全。  
  
-   已经删除了快照 ActiveX 控件。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或者使用复制存储过程以编程方式创建和管理快照。 有关详细信息，请参阅主题"如何：创建并应用初始快照 ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])"和"如何：创建初始快照 （复制 TRANSACT-SQL 编程）"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
-   分发 ActiveX 控件和合并 ActiveX 控件已废止。 对于使用复制管理对象 (RMO) 的托管代码应用程序提供了类似功能。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“同步订阅（RMO 编程）”。  
  
## <a name="see-also"></a>请参阅  
 [复制升级问题](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
