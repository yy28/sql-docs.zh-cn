---
title: "设置历史记录保持期 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
helpviewer_keywords:
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d03e90e7be142bd8ecd0b7e707885ebca1acf141
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>设置历史记录保持期 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在“分发数据库属性 - \<分发数据库>”对话框的“常规”页上指定历史记录保持期。 此设置控制复制代理历史记录可存储的时间。 可以从“分发服务器属性 - \<分发服务器>”对话框的“常规”页中访问该页。 有关访问此对话框的详细信息，请参阅[查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-history-retention-period"></a>指定历史记录保持期  
  
1.  在“分发服务器属性 - \<分发服务器>”对话框的“常规”页上，单击分发数据库的属性按钮 (**…**)。  
  
2.  在 **“至少存储复制性能的历史记录”** 框中输入一个值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [配置分发](../../relational-databases/replication/configure-distribution.md)  
  
  
