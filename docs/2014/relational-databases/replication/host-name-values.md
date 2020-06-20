---
title: HOST_NAME 值 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 67d01df05c8d56fd435eb0ee1b42ba2da6a312ce
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010540"
---
# <a name="host_name-values"></a>HOST_NAME 值
  具有参数化筛选器的合并发布使用 SUSER_SNAME() 和/或 HOST_NAME() 函数筛选数据。 函数在新建发布向导或 **“发布属性”** 对话框中指定。  
  
 默认情况下，HOST_NAME() 函数返回连接到发布服务器的计算机的名称。 在使用参数化筛选器时，通常在向导的此页上提供值来覆盖此值。 这样，HOST_NAME() 函数将返回指定的值而非计算机的名称。 有关详细信息，请参阅[参数化行筛选器](merge/parameterized-filters-parameterized-row-filters.md)的“覆盖 HOST_NAME() 值”部分。  
  
> [!NOTE]  
>  如果覆盖 HOST_NAME()，则对 HOST_NAME() 函数的所有调用将全部返回指定的值。 请确保其他应用程序未依赖于返回计算机名称的 HOST_NAME()。  
  
## <a name="options"></a>选项  
 **订阅属性**  
 在 **“HOST_NAME 值”** 列中为每个订阅服务器输入一个值或者接受默认值，默认值为订阅服务器计算机的名称。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [查看和修改请求订阅属性](view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](view-and-modify-push-subscription-properties.md)   
 [HOST_NAME (Transact-SQL)](/sql/t-sql/functions/host-name-transact-sql)   
 [订阅发布](subscribe-to-publications.md)  
  
  
