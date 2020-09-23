---
description: Resize the Job History Log
title: Resize the Job History Log
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 99a06d15025dd4a8ee6970aeb5175bbe58d4cc36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492038"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log

[!INCLUDE[applies-to-version/_ssnoversion.md](../../includes/applies-to-version/sqlserver.md)]

> [!IMPORTANT]  
> [Azure SQL 托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数（但不是所有）SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 托管实例与 SQL Server 的 T-SQL 区别](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题介绍了如何使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 代理作业历史记录日志的大小限制。

- **开始之前：**  

    [安全性](#Security)  

- **若要设置作业历史记录日志的大小限制，可使用：**  

    [SQL Server Management Studio](#SSMS)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>开始之前  

### <a name="security"></a><a name="Security"></a>安全性

有关详细信息，请参阅[实现 SQL Server 代理安全性](../../ssms/agent/implement-sql-server-agent-security.md)。  

## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio

*基于原始大小重设作业历史记录日志的大小*

1. 在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。

2. 右键单击“SQL Server 代理”，然后选择“属性” 。

3. 选择“历史记录”  页，然后确认是否已选中“限制作业历史记录日志大小”  。

4. 在 **“作业历史记录日志的最大大小”** 框中，输入作业历史记录日志允许的最大行数。

5. 在 **“每个作业的最大作业历史记录行数”** 框中，输入作业允许的作业历史记录的最大行数。

**基于时间重设作业历史记录日志的大小：**

1. 在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  

2. 右键单击“SQL Server 代理”，然后选择“属性” 。

3. 选择“历史记录”页，然后选择“删除代理历史记录” 。

4. 选择适当的“天”  、“周”  或“月”  数。
