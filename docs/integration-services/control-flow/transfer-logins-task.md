---
title: "传输登录名任务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transferloginstask.f1"
helpviewer_keywords: 
  - "传输登录名任务 [Integration Services]"
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# 传输登录名任务
  传输登录名任务在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例之间传输一个或多个登录名。  
  
## 在 SQL Server 实例之间传输登录名  
 传输登录名任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。  
  
## 事件  
 该任务将引发报告已传输的登录名数的信息事件，而且在覆盖登录名时还会引发警告事件。  
  
 传输登录名任务并不报告登录名传输的进度，它仅报告 0% 和 100 % 完成。  
  
## 执行值  
 在该任务的 **ExecutionValue** 属性中定义的执行值返回已传输的登录名数。 通过将用户定义的变量分配给传输登录名任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关登录名传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](../Topic/Use%20Variables%20in%20Packages.md)。  
  
## 日志项  
 传输登录名任务包括下列自定义日志项：  
  
-   TransferLoginsTaskStarTransferringObjects   此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferLoginsTaskFinishedTransferringObjects   此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外，还有 **OnInformation** 事件的日志项（报告已传输的登录名数），以及 **OnWarning** 事件的日志项（是为目标服务器上每个被覆盖的登录名写入的）。  
  
## 安全性和权限  
 若要浏览源服务器上的登录名并在目标服务器上创建登录名，用户必须同时是这两台服务器上 sysadmin 服务器角色的成员。  
  
## 传输登录名任务的配置  
 传输登录名任务可以配置为传输所有登录名，只传输指定登录名，或者只传输对指定的数据库具有访问权限的所有登录名。 无法传输 sa 登录名。 可以重命名 sa 登录名；但是，无法传输重命名的 sa 登录名。  
  
 您还可以指示该任务是否复制与登录名关联的安全标识符 (SID)。 如果传输登录名任务与传输数据库任务结合使用，则必须将 SID 复制到目标数据库，否则目标数据库将无法识别所传输的登录名。  
  
 在目标服务器上，所传输的登录名将被禁用，而且将分配给它们随机的密码。 目标服务器上 sysadmin 角色的成员必须更改这些密码并启用这些登录名，才能使用这些登录名。  
  
 要传输的登录名可能已经存在于目标服务器上。 传输登录名任务可以配置为以下列方式处理现有登录名：  
  
-   覆盖现有登录名。  
  
-   如果存在重复登录名，则该任务失败。  
  
-   跳过重复登录名。  
  
 在运行时，传输登录名任务使用两个 SMO 连接管理器连接到源服务器和目标服务器。 SMO 连接管理器与传输登录名任务分开进行配置，然后在传输登录名任务中引用连接管理器。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [传输登录名任务编辑器（“常规”页）](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)  
  
-   [传输登录名任务编辑器（“登录名”页）](../../integration-services/control-flow/transfer-logins-task-editor-logins-page.md)  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## 传输登录名任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
  