---
title: "HOST_NAME 值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.hostnamevalue.f1"
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# HOST_NAME 值
  具有参数化筛选器的合并发布使用 SUSER_SNAME() 和/或 HOST_NAME() 函数筛选数据。 函数在新建发布向导或 **“发布属性”** 对话框中指定。  
  
 默认情况下，HOST_NAME() 函数返回连接到发布服务器的计算机的名称。 在使用参数化筛选器时，通常在向导的此页上提供值来覆盖此值。 这样，HOST_NAME() 函数将返回指定的值而非计算机的名称。 有关详细信息，请参阅的"覆盖 host_name （） 值"部分 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
> [!NOTE]  
>  如果覆盖 HOST_NAME()，则对 HOST_NAME() 函数的所有调用将全部返回指定的值。 请确保其他应用程序未依赖于返回计算机名称的 HOST_NAME()。  
  
## 选项  
 **订阅属性**  
 在每个订阅服务器中输入的值 **HOST_NAME 值** 列，或接受默认情况下，订阅服务器计算机的名称。  
  
## 另请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)   
 [查看和修改请求订阅属性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME & #40;Transact SQL & #41;](../../t-sql/functions/host-name-transact-sql.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  