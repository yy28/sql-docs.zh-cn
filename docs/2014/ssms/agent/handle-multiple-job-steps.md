---
title: 处理多个作业步骤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- ordering job steps [SQL Server]
- multiple job steps
- SQL Server Agent jobs, job steps
- control of flow for jobs [SQL Server]
ms.assetid: 7aba19ff-72b3-45f6-8e54-23f4988d63a8
author: stevestein
ms.author: sstein
ms.openlocfilehash: fef0fb69b5bfd028977276d8efabc333a21e0feb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044561"
---
# <a name="handle-multiple-job-steps"></a>处理多个作业步骤
  如果作业有多个作业步骤，必须指定这些作业步骤的运行顺序。 这称为*流控制 * *。* 您可以随时添加新的作业步骤并重排作业步骤流，更改在下次运行作业时生效。 下图说明了一个数据库备份作业的流控制。  
  
 ![SQL Server 代理作业步骤的流控制](../../database-engine/media/dbflow01.gif "SQL Server 代理作业步骤的流控制")  
  
 第一步是备份数据库。 如果这一步失败， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将把失败报告给定义为接收通知的操作员。 如果备份数据库步骤成功，则作业将继续进行下一步，即“清理”客户端数据。 如果这一步失败， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理将向前跳至还原数据库。 如果“清理”客户端数据成功，则作业将继续进行下一步，即更新统计信息，如此继续，直至最后报告成功或报告失败。  
  
 为每个作业步骤的成功和失败都定义一个流控制操作。 必须指定作业步骤成功执行的操作和作业步骤失败时执行的操作。 还可以定义对失败的作业步骤进行重试的次数以及重试时间间隔。  
  
> [!NOTE]  
>  当使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理图形用户界面 (GUI) 并从多步骤作业中删除一个或多个步骤时，GUI 将删除所有作业步骤，然后使用正确的成功时或失败时引用重新添加剩余的步骤。 例如，假设您有一个包含五个步骤的作业，第一步配置为在顺利完成时即跳到第 4 步。 如果删除第 3 步，则 GUI 将删除此作业的所有步骤，然后使用正确的引用添加剩余的四个步骤（1、2、4 和 5）。 在此示例中，第 1 步中的引用将重新配置为在第 1 步顺利完成时即跳到第 3 步。  
  
 作业步骤必须自包含。 也就是说，作业不能在作业步骤之间传递布尔值、数据或数值。 但可以使用永久表或全局临时表在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作业步骤之间传递值。 可以使用文件在运行可执行程序的作业步骤之间传递值。 例如，一个作业步骤运行的可执行程序向一个文件写入数据，后续作业步骤运行的可执行程序读取该文件。  
  
> [!NOTE]  
>  如果创建循环作业步骤（作业步骤 1 后面跟着作业步骤 2，然后作业步骤 2 又返回到作业步骤 1），则在使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创建作业时会出现警告消息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在作业历史记录中记录作业和作业步骤信息。  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_job &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)   
 [dbo.sysjobhistory &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobhistory-transact-sql)   
 [dbo.sys作业 &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobs-transact-sql)   
 [dbo.sysjobsteps &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobsteps-transact-sql)   
 [实现作业](implement-jobs.md)   
 [管理作业步骤](manage-job-steps.md)  
  
  
