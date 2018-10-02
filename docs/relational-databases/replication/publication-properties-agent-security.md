---
title: 发布属性 - 代理安全性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
ms.assetid: 03945aac-66f2-4370-b5d1-c1de694bc4c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb56972bd63a1fbd7cd265443b0db1ad86d439c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762995"
---
# <a name="publication-properties-agent-security"></a>发布属性，代理安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以使用 **“发布属性”** 对话框的 **“代理安全性”** 页，访问运行以下代理的帐户的设置以及连接到复制拓扑中的计算机：  
  
-   所有发布的快照代理。  
  
-   所有事务发布的日志读取器代理。 对于使用事务复制发布的每个数据库，都有一个日志读取器代理。 更改日志读取器代理的设置会影响数据库中的所有事务发布。  
  
-   允许排队更新订阅的事务发布的队列读取器代理。 每个分发数据库都有一个队列读取器代理。 更改队列读取器代理的设置会影响所有具有排队更新订阅（使用相同的分发数据库）的事务发布。 有关队列读取器代理安全设置的详细信息，请参阅[查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 有关每个代理所需安全设置和权限的详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## <a name="options"></a>选项  
 **“安全设置”** 或 **“创建代理”**  
 如果已创建代理作业，那么请单击 **“安全设置”** 以访问一个对话框，在其中可以更改代理安全设置。 如果未创建代理作业，请单击 **“创建代理”** 来创建代理，并指定安全设置。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保护（复制）](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
