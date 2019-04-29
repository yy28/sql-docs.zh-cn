---
title: 设置目标服务器的轮询间隔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- interval for polling [SQL Server]
- target servers [SQL Server], polling interval
- polling interval [SQL Server]
ms.assetid: 4ffbbefa-77fb-442e-a77c-cb8c6cab9f3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1578bbefc9ae17baae56799d943e5ae6186628ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63033616"
---
# <a name="set-the-polling-interval-for-target-servers"></a>设置目标服务器的轮询间隔
  本主题介绍如何设置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理刷新从主服务器到目标服务器的信息的频率。 作业是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理执行的一系列指定操作。 多服务器作业是主服务器在一台或多台目标服务器上运行的作业。  
  
-   **开始之前：**[安全性](#Security)  
  
-   **若要设置目标服务器，使用的轮询间隔：**[SQL Server Management Studio](#SSMS)、[Transact-SQL](#TSQL)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 每个目标服务器一次只能运行一个相同作业的实例。 每台目标服务器会定期轮询主服务器，下载分配给目标服务器的任何新作业的一个副本，然后断开连接。 目标服务器在本地运行作业，然后重新连接到主服务器以上载作业结果状态。  
  
> [!NOTE]  
>  如果在目标服务器试图上载作业状态时无法访问主服务器，则作业将处于假脱机状态，直到可以访问主服务器。  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md) 和 [Choose the Right SQL Server Agent Service Account for Multiserver Environments](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
 **设置目标服务器的轮询间隔**  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”，指向“多服务器管理”，再单击“管理目标服务器”。  
  
3.  在 **“目标服务器状态”** 选项卡上，单击 **“发布指令”**。  
  
4.  在 **“指令类型”** 列表中，选择 **“设置轮询间隔”**。  
  
5.  在 **“轮询间隔”** 框中，输入介于 10 到 28,800 之间的秒数，目标服务器必须在经过该秒数后才会轮询主服务器。  
  
6.  在 **“收件人”** 下，执行以下操作之一：  
  
    1.  如果所有目标服务器共享同一轮询间隔，则单击 **“所有目标服务器”** 。  
  
    2.  如果并非所有目标服务器都共享同一轮询间隔，则单击 **“以下目标服务器”** ，然后选择将使用此轮询间隔的每台目标服务器。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
 **设置目标服务器的轮询间隔**  
  
1.  在对象资源管理器中，连接到数据库引擎实例，然后展开该实例。  
  
2.  在工具栏上，单击 **“新建查询”**。  
  
3.  在查询窗口中，使用[sp_post_msx_operation &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)系统存储过程来设置目标服务器的轮询间隔。  
  
## <a name="see-also"></a>请参阅  
 [dbo.sysdownloadlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysdownloadlist-transact-sql)  
  
  
