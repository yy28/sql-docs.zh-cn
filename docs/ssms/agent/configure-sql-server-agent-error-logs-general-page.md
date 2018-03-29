---
title: 配置 SQL Server 代理错误日志（“常规”页）| Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 813a6a89e211bd3b524b80ddf12113b6e52a817d
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>配置 SQL Server 代理错误日志（“常规”页）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此屏幕可以查看和更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理错误日志记录的设置。  
  
## <a name="options"></a>“常规”  
**错误日志文件**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理将写入错误日志的文件。  
  
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
  
## <a name="see-also"></a>另请参阅  
[SQL Server 代理错误日志](../../ssms/agent/sql-server-agent-error-log.md)  
  
