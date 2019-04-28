---
title: 分发代理的安全性（对等复制）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78d8baed7783459db79bb9facb0141cc570c4127
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721378"
---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>分发代理的安全性（对等复制）
  使用 **“分发代理安全性”** 页，可以指定运行分发代理以及与对等拓扑中的计算机建立连接时所使用的帐户。 有关代理要求的权限及复制安全的最佳做法的信息，请参阅[复制代理安全模型](security/replication-agent-security-model.md)和[复制安全最佳做法](security/replication-security-best-practices.md)。  
  
> [!NOTE]  
>  如果在上次运行此向导时已经对订阅的分发代理进行了配置，则无法更改分发代理在此向导中所使用的凭据。 如果指定新凭据，它们将被忽略。 若要更改凭据，请使用 **“订阅属性”** 对话框。 有关详细信息，请参阅 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)。  
  
## <a name="options"></a>选项  
 单击每个订阅服务器的行中的属性按钮 (**...**)，可以访问 **“分发代理安全性”** 对话框。 对于代理使用的帐户，有关其所需权限的详细信息，请在启动的 **“分发代理安全性”** 对话框中单击 **“帮助”** 。  
  
 在一个对话框中输入设置后，将在网格中显示订阅服务器的连接信息。  
  
 **订阅服务器代理**  
 每个对等方的名称。  
  
 **对等数据库**  
 对等方上同时用作发布数据库和订阅数据库的数据库。  
  
 **与分发服务器的连接**  
 连接到分发服务器时所处的上下文。 始终使用运行代理的 Windows 帐户的上下文建立本地连接： 此向导将创建推送订阅 （本地连接是与分发服务器的连接），因此此字段将始终显示：**模拟 '\<域 >\\< 登录名\>'** 或**模拟 '\<计算机 >\\< 登录名\>**。  
  
 **与订阅服务器的连接**  
 与订阅服务器建立连接时所处的上下文。 可以使用运行代理的 Windows 帐户的上下文或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的上下文建立连接。 该字段显示下列选项之一：“使用登录名‘\<登录名>’”、“模拟‘\<域>\\<登录名\>’”或“模拟‘\<计算机>\\<登录名\>’”。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用 Windows 帐户的上下文建立所有连接。  
  
## <a name="see-also"></a>请参阅  
 [管理对等拓扑（复制 Transact-SQL 编程）](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](transactional/peer-to-peer-transactional-replication.md)  
  
  
