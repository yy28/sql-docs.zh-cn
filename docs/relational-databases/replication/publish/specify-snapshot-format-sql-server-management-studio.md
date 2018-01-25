---
title: "指定快照格式 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0fa034fbebc77e66d044fcde9d68d26289cbd88e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>指定快照格式 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在“发布属性 - \<发布>”对话框的“快照”页上指定快照格式。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### <a name="to-specify-snapshot-format"></a>指定快照格式  
  
1.  在“发布属性 - \<发布>”对话框的“快照”页上，选择“本机 SQL Server - 所有订阅服务器都必须是运行 SQL Server 的服务器”或“字符 - 如果发布服务器或订阅服务器没有运行 SQL Server，则需要此项”。  
  
    > [!NOTE]  
    >  建议选择本机格式，除非此发布必须支持对 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 数据库或非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的订阅。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [配置快照属性（复制 Transact-SQL 编程）](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [使用快照初始化订阅](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
