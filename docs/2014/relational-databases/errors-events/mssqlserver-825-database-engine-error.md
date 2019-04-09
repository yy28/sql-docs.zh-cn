---
title: MSSQLSERVER_825 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9aa14c99113f00339efcc0b584a6677042679b5a
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240616"
---
# <a name="mssqlserver825"></a>MSSQLSERVER_825
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|825|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|B_RETRYWORKED|  
|消息正文|在失败 %d 次(错误: %ls)之后，按偏移量 %#016I64x 对文件“%ls”读取成功。 SQL Server 错误日志和系统事件日志中的其他消息中可能有更详细的信息。 此错误情况威胁到数据库的完整性，因此必须予以更正。 请运行一次完整的数据库一致性检查 (DBCC CHECKDB)。 此错误可能是由多种因素导致的；有关详细信息，请参阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>解释  
 此消息表明至少必须重新执行一次读取操作，且磁盘硬件存在严重问题。 此消息当前未指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 问题，但如果不解决磁盘问题，则可能会导致数据丢失或数据库损坏。 系统事件日志可能包含有助于诊断此问题的相关事件。 有关 I/O 错误的详细信息，请参阅 [Microsoft SQL Server I/O 基础知识，第 2 章](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))。  
  
## <a name="user-action"></a>用户操作  
 下列操作可帮助您识别和解决基本问题：  
  
-   查阅错误日志和此消息中的变量文本以获得说明问题的线索。  
  
-   检查磁盘系统。 此问题可能与磁盘、磁盘控制器、阵列卡或磁盘驱动程序有关。  
  
-   与磁盘制造商联系以获得用于检查磁盘系统状态的最新实用工具。  
  
-   与磁盘制造商联系以获得最新的驱动程序。  
  
  
