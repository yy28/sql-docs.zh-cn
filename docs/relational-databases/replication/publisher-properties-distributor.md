---
title: "发布服务器属性 - 分发服务器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.configdistwizard.distpubproperties.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: ab6ada76-0f99-43fe-b524-baac7b1bc483
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdbb73e5adcb6da6ba31ab69cfdc99840507fd80
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="publisher-properties---distributor"></a>发布服务器属性 - 分发服务器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 **“发布服务器属性”** 对话框，可以查看和修改与发布服务器和其分发服务器之间的关系相关联的属性。  
  
## <a name="options"></a>“常规”  
 **到发布服务器的代理连接**  
 指定以下代理从分发服务器连接到发布服务器时所处的上下文：  
  
-   允许排队更新订阅的事务发布的队列读取器代理。  
  
-   用于 Oracle 发布的快照代理和日志读取器代理。  
  
 选择 **“模拟代理进程帐户”** 以使用运行这些代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的上下文连接到发布服务器，或指定 **“SQL Server 身份验证”**，然后为 **“登录名”** 和 **“密码”**输入值。 建议选择 **“模拟代理进程帐户”**。 有关代理安全性的详细信息，请参阅[复制代理安全模式](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 在新建发布向导中可以指定运行这些代理的 Windows 帐户。 您可以在如下位置更改这些帐户：  
  
-   队列读取器代理的 **“分发服务器属性”** 对话框。  
  
-   快照代理和日志读取器代理的 **“发布属性”** 对话框。  
  
 **杂项**  
 **“发布服务器类型”** 和 **“分发数据库名称”** 都是只读属性。 可以更改 **“默认快照文件夹”** 属性。 有关快照文件夹的详细信息，请参阅[保护快照文件夹](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [属性参考（复制）](../../relational-databases/replication/properties-reference-replication.md)  
  
  
