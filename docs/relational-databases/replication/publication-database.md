---
title: 发布数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.publicationdatabase.f1
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c45fc60ea01d741d2db1a308d127d555bbce95b
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351649"
---
# <a name="publication-database"></a>发布数据库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  发布数据库是发布服务器上的数据库，它是要复制的数据和数据库对象的源。 必须启用复制操作中使用的每个发布数据库。 当 **sysadmin** 固定服务器角色成员执行以下任一操作时，即可启用相应的数据库：  
  
-   使用新建发布向导对该数据库创建发布。  
  
-   在 **“发布服务器属性”** 对话框中选择该数据库。  
  
-   执行 **sp_replicationdboption** ，并将 **publish** （对于快照发布或事务发布）或 **merge publish** （对于合并发布）选项设置为 **True**。  
  
## <a name="options"></a>“常规”  
 **数据库**  
 选择包含要发布的数据和数据库对象的数据库名称。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)  
  
  
