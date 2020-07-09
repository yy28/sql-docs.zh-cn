---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1d71b87d3927e2b79d2147099c50581a3687e32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767829"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|833|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|BUF_LONG_IO|  
|消息正文|SQL Server 已 %d 次遇到了针对数据库 `[%ls] (%d)` 中文件 [%ls] 的、所需完成时间超过 %d 秒的 I/O 请求。  OS 文件句柄是 0x%p。  最新的长时间 I/O 操作的偏移量是: %#016I64x。|  
  
## <a name="explanation"></a>说明  
该消息指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已从磁盘发出读取或写入请求，并且表明该请求返回所用的时间已超过 15 秒。 该错误由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 报告，表明 IO 子系统有问题。  
  
### <a name="possible-causes"></a>可能的原因  
这种问题可能是由于系统性能问题、硬件错误、固件错误、设备驱动程序问题或 IO 进程中的筛选器驱动程序干预引起的。  
  
## <a name="user-action"></a>用户操作  
通过检查系统事件日志获得硬件相关错误消息来纠正引错误。 并且，如果有特定于硬件的日志，也要进行检查。  
  
使用性能监视器检查以下计数器：  
  
-   **Average Disk Sec/Transfer**  
  
-   **Average Disk Queue Length**  
  
-   **Current Disk Queue Length**  
  
例如，运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的 **Average Disk Sec/Transfer** 时间通常少于 15 毫秒。 如果 **Average Disk Sec/Transfer** 值增加，这表明 I/O 子系统未能完全满足 I/O 需求。  
  
> [!NOTE]  
> 防病毒程序可能会减慢磁盘访问速度。 若要提高访问速度，请将错误消息中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据文件从实时病毒扫描中排除。  
  
有关 I/O 错误的详细信息，请参阅 [Microsoft SQL Server I/O 基础知识，第 2 章](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))以及 [https://support.microsoft.com/kb/897284/en-us](https://support.microsoft.com/kb/897284/en-us) 上的知识库文章。  
  
