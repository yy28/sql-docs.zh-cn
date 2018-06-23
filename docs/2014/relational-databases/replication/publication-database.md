---
title: 发布数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newpubwizard.publicationdatabase.f1
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cb4f3f0e770b1511145f079908e0fd019d1b0c57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026968"
---
# <a name="publication-database"></a>发布数据库
  发布数据库是发布服务器上的数据库，它是要复制的数据和数据库对象的源。 必须启用复制操作中使用的每个发布数据库。 当 **sysadmin** 固定服务器角色成员执行以下任一操作时，即可启用相应的数据库：  
  
-   使用新建发布向导对该数据库创建发布。  
  
-   在 **“发布服务器属性”** 对话框中选择该数据库。  
  
-   执行 **sp_replicationdboption** ，并将 **publish** （对于快照发布或事务发布）或 **merge publish** （对于合并发布）选项设置为 **True**。  
  
## <a name="options"></a>“常规”  
 **数据库**  
 选择包含要发布的数据和数据库对象的数据库名称。  
  
## <a name="see-also"></a>请参阅  
 [发布数据和数据库对象](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)  
  
  
