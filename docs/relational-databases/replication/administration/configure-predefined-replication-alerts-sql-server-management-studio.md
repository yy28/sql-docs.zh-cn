---
title: "配置预定义的复制警报 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "警报 [SQL Server 复制]"
  - "预定义的复制警报 [SQL Server 复制]"
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 配置预定义的复制警报 (SQL Server Management Studio)
  复制提供了下列预定义警报，可以配置这些警报以响应复制事件：  
  
-   **复制: 代理成功**  
  
-   **复制: 代理失败**  
  
-   **复制：代理重试**  
  
-   **复制：已删除过期的订阅**  
  
-   **复制：验证失败后重新初始化了订阅**  
  
-   **复制：订阅服务器未通过数据验证**  
  
-   **复制：订阅服务器已通过数据验证**  
  
-   **复制：代理自定义关闭**  
  
 在  中的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 文件夹或复制监视器的 **“警告”** 选项卡中配置这些警报。 有关访问此选项卡的详细信息，请参阅 [查看信息和订阅和 #40; 执行的任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)。  
  
 除这些警报之外，复制监视器还提供了一组与状态和性能相关的警告和警报。 有关详细信息，请参阅 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。 您也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 警报基础结构为其他复制事件定义警报。 有关详细信息，请参阅 [创建用户定义事件](../../../ssms/agent/create-a-user-defined-event.md)。  
  
### 在 Management Studio 中配置预定义复制警报  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，然后展开 **“警报”** 文件夹。  
  
3.  右键单击一个复制警报，，然后单击 **属性**。  
  
4.  在设置选项 **\< AlertName> 警报属性** 对话框中︰  
  
    -   在 **“常规”** 页上，单击 **“启用”**，指定应用此警报的数据库。  
  
    -   在 **响应** 页上，指定是否应发送一封电子邮件和/或应执行作业。  
  
         如果警报为 **复制︰ 订阅服务器未通过数据验证**, ，您可以指定响应作业复制提供了此警报︰ 选择 **执行作业**, ，然后单击浏览按钮 (**...**)。 在 **“定位作业”** 对话框中，单击 **“浏览”**。 在 **“查找对象”** 对话框中，选择 **“重新初始化未通过数据验证的订阅”**。 在两个打开的对话框中，单击 **“确定”** 。 作业执行时，它将把远程过程调用 (RPC) 用于重新初始化订阅的存储过程。 如果发布服务器使用远程分发服务器，您必须在发布服务器上定义远程服务器登录名，以便可以从分发服务器到发布服务器进行 RPC。  
  
    -   在 **“选项”** 页上，自定义响应文本。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### 在复制监视器中配置阈值的警报  
  
1.  在 **“警告”** 选项卡上，单击 **“配置警报”**。  
  
2.  在 **“配置复制警报”** 对话框中，选择一个警报，然后单击 **“配置”**。  
  
3.  在设置选项 **\< AlertName> 警报属性** 对话框中︰  
  
    -   在 **“常规”** 页上，单击 **“启用”**，指定应用此警报的数据库。  
  
    -   在 **响应** 页上，指定是否应发送一封电子邮件和/或应执行作业。  
  
         如果警报为 **复制︰ 订阅服务器未通过数据验证**, ，您可以指定响应作业复制提供了此警报︰ 选择 **执行作业**, ，然后单击浏览按钮 (**...**)。 在 **“定位作业”** 对话框中，单击 **“浏览”**。 在 **“查找对象”** 对话框中，选择 **“重新初始化未通过数据验证的订阅”**。 在两个打开的对话框中，单击 **“确定”** 。 作业执行时，它将把远程过程调用 (RPC) 用于重新初始化订阅的存储过程。 如果发布服务器使用远程分发服务器，您必须在发布服务器上定义远程服务器登录名，以便可以从分发服务器到发布服务器进行 RPC。  
  
    -   在 **“选项”** 页上，自定义响应文本。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  单击 **“关闭”**。  
  
## 另请参阅  
 [对复制代理事件使用警报](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  