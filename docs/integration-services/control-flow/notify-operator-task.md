---
title: "通知操作员任务 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb791195dccb44add2d1b196e33e03d3a45d7049
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="notify-operator-task"></a>“通知操作员”任务
  “通知操作员”任务将通知消息发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理操作员。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理操作员是可以接收电子通知的人或组的别名。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作员的详细信息，请参阅 [操作员](http://msdn.microsoft.com/library/38e8488f-2669-4cea-b9c3-5f394a663678)。  
  
 通过使用“通知操作员”任务，包可以通过电子邮件、寻呼程序或 **net send**通知一个或多个操作员。 可以用不同的方式通知各个操作员。 例如，用电子邮件和寻呼程序通知操作员 A，而用寻呼程序和 **net send**通知操作员 B。 接收来自此任务的通知的操作员必须是“通知操作员”任务的 **OperatorNotify** 集合的成员。  
  
 “通知操作员”任务是唯一一个不封装 Transact-SQL 语句或 DBCC 命令的数据库维护任务。  
  
## <a name="configuration-of-the-notify-operator-task"></a>“通知操作员”任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“通知操作员”任务（维护计划）](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
