---
title: "HOST_NAME 值 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c8175cd22da36e5b07c0c7b0807701d64df3d8d8
ms.lasthandoff: 04/11/2017

---
# <a name="hostname-values"></a>HOST_NAME 值
  具有参数化筛选器的合并发布使用 SUSER_SNAME() 和/或 HOST_NAME() 函数筛选数据。 函数在新建发布向导或 **“发布属性”** 对话框中指定。  
  
 默认情况下，HOST_NAME() 函数返回连接到发布服务器的计算机的名称。 在使用参数化筛选器时，通常在向导的此页上提供值来覆盖此值。 这样，HOST_NAME() 函数将返回指定的值而非计算机的名称。 有关详细信息，请参阅[参数化行筛选器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)的“覆盖 HOST_NAME() 值”部分。  
  
> [!NOTE]  
>  如果覆盖 HOST_NAME()，则对 HOST_NAME() 函数的所有调用将全部返回指定的值。 请确保其他应用程序未依赖于返回计算机名称的 HOST_NAME()。  
  
## <a name="options"></a>选项  
 **订阅属性**  
 在 **“HOST_NAME 值”** 列中为每个订阅服务器输入一个值或者接受默认值，默认值为订阅服务器计算机的名称。  
  
## <a name="see-also"></a>另请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [查看和修改请求订阅属性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME (Transact-SQL)](../../t-sql/functions/host-name-transact-sql.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
