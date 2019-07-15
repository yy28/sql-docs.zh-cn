---
title: 为作业选取计划 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 31b7df7f6c5441f31931aa78ad20a59b0a9840de
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67685488"
---
# <a name="pick-schedule-for-job"></a>为作业选取计划
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此对话框可以为 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业选取现有的计划。  
  
## <a name="options"></a>选项  
**可用计划**  
列出此作业的可用计划。 因为作业和计划必须具有相同的所有者，所以，此列表只包括该作业的所有者所拥有的计划。  
  
**名称**  
显示计划的名称。  
  
**已启用**  
如果计划处于启用状态，则选中该选项。  
  
**Description**  
描述计划运行作业的条件。  
  
**计划中的作业**  
列出附加到计划的作业编号。 单击编号可以查看相应作业的属性。  
  
**属性**  
启动“作业计划属性”  对话框，可以在该对话框中查看该计划的有关信息。  
  
## <a name="see-also"></a>另请参阅  
[创建计划并将计划附加到作业](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
