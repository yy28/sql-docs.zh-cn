---
description: 日志传送监视器设置
title: 日志传送监视器设置 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
ms.openlocfilehash: 33ff5abf38eef7525dff17587a32529ddddc689b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465435"
---
# <a name="log-shipping-monitor-settings"></a>日志传送监视器设置
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  使用此页可以配置和修改日志传送监视服务器的属性。  
  
 有关日志传送概念的说明，请参阅 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。  
  
## <a name="options"></a>选项  
 **监视服务器实例**  
 显示在日志传送配置中当前配置为监视服务器的服务器实例的名称。  
  
 **“连接”**  
 选择并连接到用作监视服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 用于连接的帐户必须是辅助服务器实例上 sysadmin 固定服务器角色的成员。  
  
 **模拟作业的代理帐户**  
 在连接到监视服务器实例时，让日志传送模拟 SQL Server 代理的代理帐户。 备份、复制和还原进程必须能够连接到监视服务器，才可更新日志传送操作的状态。  
  
 **使用以下 SQL Server 登录名**  
 在连接到监视服务器实例时，允许日志传送使用特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 备份、复制和还原进程必须能够连接到监视服务器，才可更新日志传送操作的状态。 如果希望日志传送使用特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，请选择此选项，然后指定登录名和密码。  
  
 **在以下时间后删除历史记录**  
 指定在删除日志传送历史记录信息之前，该信息在监视服务器上保留的时间。  
  
 **作业名称**  
 指示 SQL Server 代理警报作业的名称，日志传送使用该作业在超出备份或还原阈值时发出警报。 首次创建此作业时，可以通过在该框中键入内容来更改名称。  
  
 **计划**  
 指示 SQL Server 代理警报作业的当前计划。  
  
 **编辑**  
 修改 SQL Server 代理警报作业的参数。  
  
 **禁用此作业**  
 挂起 SQL Server 代理警报作业。  
  
  
