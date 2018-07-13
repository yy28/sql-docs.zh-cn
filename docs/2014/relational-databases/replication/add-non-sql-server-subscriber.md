---
title: 添加非 SQL Server 订阅服务器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53575d47aa541ec59a3c9e3003795c5321f6f0d3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157948"
---
# <a name="add-non-sql-server-subscriber"></a>添加非 SQL Server 订阅服务器
  复制支持创建对 Oracle 和 IBM DB2 订阅服务器的快照和事务发布的推送订阅。  
  
## <a name="options"></a>“常规”  
 **要添加的订阅服务器类型**  
 选择 Oracle 订阅服务器或 IBM DB2 订阅服务器。 有关对这些订阅服务器的支持的详细信息，请参阅[非 SQL Server 订阅服务器](non-sql/non-sql-server-subscribers.md)。  
  
 **数据源名称**  
 用于在网络上定位数据库的名称。 复制使用数据源名称以及在此向导的 **“分发代理安全性”** 页中指定的登录名、密码和所有连接选项，来为数据库生成连接字符串。  
  
> [!NOTE]  
>  The data source name and connection string are not validated by [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] until the Distribution Agent attempts to initialize the subscription.  
  
## <a name="see-also"></a>请参阅  
 [为非 SQL Server 订阅服务器创建订阅](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
