---
title: MSSQLSERVER - 数据库引擎错误 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8a678fe4fdda95710b6e6707f922a9d0c1c9d732
ms.sourcegitcommit: a02727aab143541794e9cfe923770d019f323116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75755876"
---
# <a name="mssqlserver---database-engine-error"></a>MSSQLSERVER - 数据库引擎错误
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|823|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|B_HARDERR|  
|消息正文|在文件 '%ls' 中、偏移量为 %#016I64x 的位置执行 %S_MSG 期间，操作系统已经向 SQL Server 返回了错误 %ls。 SQL Server 错误日志和系统事件日志中的其他消息中可能有更详细的信息。 这是一个威胁数据库完整性的严重系统级错误条件，必须立即纠正。 请运行一次完整的数据库一致性检查 (DBCC CHECKDB)。 此错误可能是由多种因素导致的；有关详细信息，请参阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>说明  
Windows 读取或写入请求失败。 将 Windows 返回的错误代码和相应的文本插入到消息中。 对于读取操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已经重试读取请求四次。 通常是硬件错误导致此错误，但也可能是设备驱动程序导致的。 有关错误 823 的详细信息，请参阅[错误消息 823 可能指示 SQL Server 中存在硬件或系统问题](https://support.microsoft.com/kb/828339)。 有关 I/O 错误的详细信息，请参阅 [Microsoft SQL Server I/O 基础知识，第 2 章](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))。  
  
## <a name="user-action"></a>用户操作  
查看系统事件日志中的其他信息。 与硬件制造商或 Microsoft 客户服务与支持部门联系，以确定原因和纠正操作。 在修复硬件错误后，还原所有数据库并运行 DBCC CHECKDB。  
  
