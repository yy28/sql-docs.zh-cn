---
title: 执行作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8c2e85b77997e0bba765a1c877311e1336364eaa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044984"
---
# <a name="implement-jobs"></a>执行作业
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业来自动执行日常管理任务并反复运行它们，从而提高管理效率。  
  
 作业是一系列由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理按顺序执行的指定操作。 作业可以执行一系列活动，包括运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本、命令行应用程序、Microsoft ActiveX 脚本、Integration Services 包、Analysis Services 命令和查询或复制任务。 作业可以运行重复任务或那些可计划的任务，它们可以通过生成警报来自动通知用户作业状态，从而极大地简化了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理。  
  
 可以手动运行作业，也可以将作业配置为根据计划或响应警报来运行。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**说明**|**标题**|  
|包含有关创建作业和分配所有权的信息。|[创建作业](create-jobs.md)|  
|包含有关将作业组织到目录的信息。|[组织作业](organize-jobs.md)|  
|说明可以创建的各种作业步骤以及如何管理它们。|[管理作业步骤](manage-job-steps.md)|  
|说明如何定义作业的开始运行时间和运行频率。|[创建计划并将计划附加到作业](create-and-attach-schedules-to-jobs.md)|  
|介绍手动运行作业（不根据计划）。|[运行作业](run-jobs.md)|  
|说明如何将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理配置为响应作业。 例如，可以将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理配置为作业完成时通知管理员。|[指定作业响应](specify-job-responses.md)|  
|包含有关如何查看现有作业、作业执行后的历史记录以及如何修改现有作业的信息。|[查看或修改作业](view-or-modify-jobs.md)|  
|包含有关如何删除作业的信息。|[删除作业](delete-jobs.md)|  
  
## <a name="see-also"></a>另请参阅  
 [实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)  
  
  
