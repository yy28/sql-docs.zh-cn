---
description: 添加非 SQL Server 订阅服务器
title: 添加非 SQL Server 订阅服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b2bb31950f257054279fc9d9ad354f48b50b9ca4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423651"
---
# <a name="add-non-sql-server-subscriber"></a>添加非 SQL Server 订阅服务器
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  复制支持创建对 Oracle 和 IBM DB2 订阅服务器的快照和事务发布的推送订阅。  
  
## <a name="options"></a>选项  
 **要添加的订阅服务器类型**  
 选择 Oracle 订阅服务器或 IBM DB2 订阅服务器。 有关对这些订阅服务器的支持的详细信息，请参阅[非 SQL Server 订阅服务器](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
 **数据源名称**  
 用于在网络上定位数据库的名称。 复制使用数据源名称以及在此向导的 **“分发代理安全性”** 页中指定的登录名、密码和所有连接选项，来为数据库生成连接字符串。  
  
> [!NOTE]
>  在分发代理尝试初始化订阅之前， [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能验证数据源名称和连接字符串。  
  
## <a name="see-also"></a>另请参阅  
 [为非 SQL Server 订阅服务器创建订阅](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
