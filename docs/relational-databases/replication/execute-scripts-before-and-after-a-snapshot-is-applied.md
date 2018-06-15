---
title: 在应用快照之前和之后执行脚本 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3d69aaefe439feea910c62b1aff36ebe38e402a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32956182"
---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied"></a>在应用快照之前和之后执行脚本
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在“发布属性 - \<发布>”对话框的“快照”页上，指定在应用快照前后执行的可选脚本。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
> [!NOTE]  
>  如果 **“快照格式”** 选项的设置为 **“字符”**，则这些选项不可用。  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>在应用快照前后执行脚本  
  
1.  在“发布属性 - \<发布>”对话框的“快照”页上：  
  
    -   若要指定在应用快照之前执行的脚本，请单击 **“浏览”** 导航到该脚本，或者在 **“应用快照之前执行此脚本”** 文本框中输入该脚本的路径。  
  
        > [!NOTE]  
        >  分发代理或合并代理必须对指定目录具有读取权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\scripts\myscript.sql。  
  
    -   若要指定在应用快照之后执行的脚本，请单击 **“浏览”** 导航到该脚本，或者在 **“应用快照之后执行此脚本”** 文本框中输入该脚本的 UNC 路径。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [配置快照属性（复制 Transact-SQL 编程）](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [更改发布和项目属性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [在应用快照之前和之后执行脚本](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
