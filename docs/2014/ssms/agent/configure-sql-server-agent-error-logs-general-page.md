---
title: 配置 SQL Server 代理错误日志（“常规”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d93b5f0229d4a91548588c4c562f419961f3cbc9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182917"
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>配置 SQL Server 代理错误日志（“常规”页）
  使用此屏幕可以查看和更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志记录的设置。  
  
## <a name="options"></a>选项  
 **错误日志文件**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将写入错误日志的文件。  
  
 **...**  
 浏览至错误日志文件。  
  
 **写入 OEM 错误日志**  
 以非 Unicode 文件的形式编写错误日志文件。 这可以减少日志文件占用的磁盘空间量。 不过，如果启用此选项，读取包含 Unicode 数据的消息时会有一定的难度。  
  
 **错误**  
 仅将错误和信息性消息写入日志文件。  
  
 **警告**  
 仅将警告和信息性消息写入日志文件。  
  
 **信息**  
 仅将信息性消息写入日志文件。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理错误日志](sql-server-agent-error-log.md)  
  
  
