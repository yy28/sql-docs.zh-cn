---
title: "分发代理的安全性（对等复制）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cca409052d10cc153417c1bd984273e1cad4bb9a
ms.lasthandoff: 04/11/2017

---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>分发代理的安全性（对等复制）
  使用 **“分发代理安全性”** 页，可以指定运行分发代理以及与对等拓扑中的计算机建立连接时所使用的帐户。 有关代理要求的权限及复制安全的最佳做法的信息，请参阅[复制代理安全模型](../../relational-databases/replication/security/replication-agent-security-model.md)和[复制安全最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
> [!NOTE]  
>  如果在上次运行此向导时已经对订阅的分发代理进行了配置，则无法更改分发代理在此向导中所使用的凭据。 如果指定新凭据，它们将被忽略。 若要更改凭据，请使用 **“订阅属性”** 对话框。 有关详细信息，请参阅 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
## <a name="options"></a>选项  
 单击每个订阅服务器的行中的属性按钮 (**...**)，可以访问 **“分发代理安全性”** 对话框。 对于代理使用的帐户，有关其所需权限的详细信息，请在启动的 **“分发代理安全性”** 对话框中单击 **“帮助”** 。  
  
 在一个对话框中输入设置后，将在网格中显示订阅服务器的连接信息。  
  
 **订阅服务器代理**  
 每个对等方的名称。  
  
 **对等数据库**  
 对等方上同时用作发布数据库和订阅数据库的数据库。  
  
 **与分发服务器的连接**  
 连接到分发服务器时所处的上下文。 始终使用运行代理的 Windows 帐户的上下文建立本地连接： 此向导将创建推送订阅（本地连接是与分发服务器的连接），因此，此字段将始终显示：“模拟‘\<域>\\<登录名\>’”或“模拟‘\<计算机>\\<登录名\>’”。  
  
 **与订阅服务器的连接**  
 与订阅服务器建立连接时所处的上下文。 可以使用运行代理的 Windows 帐户的上下文或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 此字段显示以下内容之一：“使用登录名‘\<登录名>’”、“模拟‘\<域>\\<登录名\>’”或“模拟‘\<计算机>\\<登录名\>’”。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
## <a name="see-also"></a>另请参阅  
 [管理对等拓扑（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [对等事务复制](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
