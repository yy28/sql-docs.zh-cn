---
title: "Oracle 发布服务器 | Microsoft Docs"
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
- sql13.rep.newpubwizard.selectoraclepublisher.f1
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de65fad508e62dc2dcd09932d1a99263193f6229
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="oracle-publisher"></a>Oracle 发布服务器
  从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的快照复制和事务复制从 Oracle 数据库中发布数据。 有关详细信息，请参阅 [Oracle 发布概述](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
 Oracle 发布服务器必须使用远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分发服务器；必须在安装和测试必需的 Oracle 网络软件之后在该服务器上运行此向导。 有关详细信息，请参阅[配置 Oracle 发布服务器](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
> [!IMPORTANT]  
>  如果其他管理员将 Oracle 数据库配置为发布服务器，那么在单击 **“下一步”** 后，将提示您输入用于连接到 Oracle 数据库的复制登录密码。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 随后会在您的登录名和 Oracle 数据库的链接服务器连接之间创建映射。 以后连接到 Oracle 数据库时无需输入密码。  
  
## <a name="options"></a>选项  
 **Oracle 发布服务器**  
 从列表中选择 Oracle 发布服务器。 此列表包含一些特定的 Oracle 发布服务器，这些服务器以前已被配置为使用运行向导的服务器作为其分发服务器。 如果列表为空，或您希望使用的 Oracle 发布服务器不在列表中，那么请单击 **“添加 Oracle 发布服务器”**。  
  
 **“添加 Oracle 发布服务器”**  
 单击此项可启动 **“分发服务器属性”** 对话框。 在此对话框中，单击 **“添加”**，再单击 **“添加 Oracle 发布服务器”**。 在 **“连接到服务器”** 对话框中，指定 Oracle 服务器名称，以及复制管理用户架构的登录名和密码。 有关详细信息，请参阅[连接到服务器 (Oracle) - 登录名](../../relational-databases/replication/connect-to-server-oracle-login.md)。  
  
> [!NOTE]  
>  如果运行向导的服务器尚未被配置为分发服务器，那么将会提示您立即进行配置。  
  
## <a name="see-also"></a>另请参阅  
 [从 Oracle 数据库创建发布](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)   
 [属性参考（复制）](../../relational-databases/replication/properties-reference-replication.md)  
  
  
