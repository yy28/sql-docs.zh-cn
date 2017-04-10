---
title: "查看和解决合并发布的数据冲突 (SQL Server Management Studio) | Microsoft Docs"
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
  - "合并复制冲突解决 [SQL Server 复制], 查看冲突"
  - "查看冲突信息"
  - "冲突解决 [SQL Server 复制], 合并复制"
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 查看和解决合并发布的数据冲突 (SQL Server Management Studio)
  可以根据为每个项目指定的冲突解决程序来解决合并发布中的冲突。 默认情况下，解决冲突无需用户干预。 但是，可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 复制冲突查看器中查看冲突，并更改解决的结果。  
  
 在冲突保持期的指定时间（默认值为 14 天）内，可以在复制冲突查看器中查看冲突数据。 若要设置冲突保持期，请执行以下任一操作：  
  
-   指定保持值 **@conflict_retention** 参数 [sp_addmergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。  
  
-   将值指定为 **conflict_retention** 为 **@property** 参数，保留值 **@value** 参数 [sp_changemergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。  
  
 默认情况下，冲突信息存储在下列位置：  
  
-   如果发布兼容级别为 90RTM 或更高，则存储在发布服务器和订阅服务器上。  
  
-   如果发布兼容级别低于 80RTM，则存储在发布服务器上。  
  
-   如果订阅服务器运行的是 [!INCLUDE[ssEW](../../includes/ssew-md.md)]，则存储在发布服务器上。 冲突数据不能存储在 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器上。  
  
 冲突信息的存储由控制 **conflict_logging** 发布属性。 有关详细信息，请参阅 [sp_addmergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 和 [sp_changemergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。  
  
 也可以在同步过程中使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 交互式冲突解决程序以交互方式解决冲突。 交互式冲突解决程序可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步管理器获取。 有关详细信息，请参阅 [同步订阅使用 Windows 同步管理器和 #40;Windows 同步管理器和 #41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)。  
  
### 查看和解决合并发布的冲突  
  
1.  连接到发布服务器 （或订阅服务器，如果适用） 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击您要为其查看冲突，并单击的发布 **查看冲突**。  
  
    > [!NOTE]  
    >  如果指定的值为 **'subscriber'** 为 **conflict_logging** 属性， **查看冲突** 菜单选项不可用。 若要查看冲突，请在命令提示符下启动 ConflictViewer.exe。 默认情况下，ConflictViewer.exe 位于以下目录中：Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE。 要获取有效引导参数的列表，请运行 ConflictViewer.exe -?。  
  
4.  在 **“选择冲突表”** 对话框中，选择要查看冲突的数据库、发布和表。  
  
5.  在复制冲突查看器中可以：  
  
    -   使用上部网格右侧的按钮来筛选行。  
  
    -   在上部网格中选择行，以在下部网格中显示该行的信息。  
  
    -   在上部网格中，选择一个或多个行，然后单击 **删除**, ，等效于单击 **提交入选方** （无需对数据进行任何更改） 的按钮。  
  
    -   单击属性按钮 (**...**) 可以对列中查看详细信息冲突中涉及。  
  
    -   在中编辑数据 **冲突解决入选方** 或 **冲突解决落选方** 专栏文章，然后提交的数据 （数据是只读的如果列为灰色）。  
  
    -   单击 **“提交入选方”** 接受指定为冲突入选方的行。  
  
    -   单击 **“提交落选方”** 覆盖解决结果，并将指定为冲突落选方的值传播到拓扑中的所有节点。  
  
    -   选择 **“记录此冲突的详细信息”** 将冲突数据记录到一个文件中。 若要指定文件的位置，请指向 **“查看”** 菜单，然后单击 **“选项”**。 输入一个值，或单击浏览按钮 (**...**)，然后导航到相应的文件。 单击 **“确定”** 可退出 **“选项”** 对话框。  
  
6.  关闭复制冲突查看器。  
  
## 另请参阅  
 [高级合并复制冲突的检测和解决](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [指定合并项目冲突解决程序](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  