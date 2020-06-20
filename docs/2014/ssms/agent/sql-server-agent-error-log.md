---
title: SQL Server 代理错误日志 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
author: stevestein
ms.author: sstein
ms.openlocfilehash: 29bc8faa8fbd897a9bbb3a51c1042d48e84ff977
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058772"
---
# <a name="sql-server-agent-error-log"></a>SQL Server 代理错误日志
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认情况下，代理创建错误日志来记录警告和错误。 日志中显示下列警告和错误：  
  
-   警告消息，提供有关潜在问题的信息，例如 "作业 \<*job_name*> 在运行时被删除"。  
  
-   错误消息，通常需要系统管理员干预，例如“无法启动邮件会话”。 可以通过 **net send**将错误消息发送给特定用户或计算机。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最多可以维护九个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志。 每个存档日志都有一个扩展名，指示该日志的相对存在时间。 例如，扩展名 .1 表示最新的存档错误日志，而扩展名 .9 表示最旧的存档错误日志。  
  
 默认情况下，执行跟踪消息不写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理日志错误，因为它们会将日志填满。 如果错误日志已满，会降低选择和分析更严重的错误的能力。 因为日志会增加服务器的处理负荷，所以请务必仔细考虑是否值得将执行跟踪消息捕获到错误日志中。 通常，最好仅在调试某个特定问题时捕获所有消息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理停止后，可以修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志的位置。 如果错误日志为空，则无法打开日志。 可以随时循环访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理日志，无需停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。  
  
 **查看 SQL Server 代理错误日志**  
  
-   [查看 SQL Server 代理错误日志 (SQL Server Management Studio)](view-sql-server-agent-error-log-sql-server-management-studio.md) 
  
 **重命名 SQL Server 代理错误日志**  
  
-   [重命名 SQL Server 代理错误日志 (SQL Server Management Studio)](rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
 **发送 SQL Server 代理错误消息**  
  
-   [发送 SQL Server 代理错误消息](send-sql-server-agent-error-messages.md)  
  
 **将执行跟踪消息写入到 SQL Server 代理错误日志中**  
  
-   [将执行跟踪消息写入到 SQL Server 代理错误日志中 (SQL Server Management Studio)](write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
  
