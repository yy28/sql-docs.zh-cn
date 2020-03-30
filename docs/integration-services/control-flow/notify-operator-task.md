---
title: “通知操作员”任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 30f1707c8d326942d2247bd3bcab31cdc38ab133
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294035"
---
# <a name="notify-operator-task"></a>“通知操作员”任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  “通知操作员”任务将通知消息发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理操作员。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理操作员是可以接收电子通知的人或组的别名。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作员的详细信息，请参阅 [操作员](../../ssms/agent/operators.md)。  
  
 通过使用“通知操作员”任务，包可以通过电子邮件、寻呼程序或 **net send**通知一个或多个操作员。 可以用不同的方式通知各个操作员。 例如，用电子邮件和寻呼程序通知操作员 A，而用寻呼程序和 **net send**通知操作员 B。 接收来自此任务的通知的操作员必须是“通知操作员”任务的 **OperatorNotify** 集合的成员。  
  
 “通知操作员”任务是唯一一个不封装 Transact-SQL 语句或 DBCC 命令的数据库维护任务。  
  
## <a name="configuration-of-the-notify-operator-task"></a>“通知操作员”任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“通知操作员”任务（维护计划）](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
