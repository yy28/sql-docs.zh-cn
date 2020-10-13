---
title: SQL Server 资源运行状况故障排除（SQL Server 实用工具）| Microsoft Docs
description: 了解 SQL Server UCP 标识的资源运行状况问题的故障排除，如使用过度的 CPU、文件空间或已分配磁盘空间。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c6c6d499d485941d490848b68b5c8142edd0cb4b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810674"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>SQL Server 资源运行状况故障排除（SQL Server 实用工具）
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  排除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 标识的资源运行状况问题可能包括缓解计算机上或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例上使用过度的 CPU，或者缓解数据层应用程序的使用过度的 CPU。 其他问题可能包括解决数据库文件的使用过度的文件空间或者解决存储卷上分配的磁盘空间的使用过度问题。  
  
 注意，如果数据库处于“紧急”状态，则运行状态将显示日志文件空间使用过度。  
  
 有关导致 UCP 上托管实例列表视图中灰色状态图标的失败的数据收集的详细信息，请参阅 [SQL Server 实用工具故障排除](/previous-versions/sql/sql-server-2016/ee210592(v=sql.130))。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具入门的详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
 有关缓解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 标识的特定资源运行状况问题的详细信息，请参阅以下主题：  
  
-   [如何识别 SQL Server 的版本](https://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [排除 SQL Server 2008 中的性能问题](/previous-versions/sql/sql-server-2008/dd672789(v=sql.100))  
  
