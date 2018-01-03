---
title: "游标和锁定特征 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: decfe9ec172e1446c8af78fbea5d534ad98e2985
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="cursor-and-lock-characteristics"></a>游标和锁定特征
游标的特性取决于提供程序的功能，而以下优点和缺点通常适用于各种类型的游标和锁定。  
  
|光标或锁定类型|优点|缺点|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-低资源要求|-不能向后滚动<br />-无数据并发|  
|**adOpenStatic**|-可滚动|-无数据并发|  
|**adOpenKeyset**|的某些数据并发<br />-可滚动|较高的资源要求<br />的在断开连接的方案中不可用|  
|**adOpenDynamic**|-高数据并发<br />-可滚动|最大资源要求<br />的在断开连接的方案中不可用|  
|**adLockReadOnly**|-低资源要求<br />-高度的可伸缩性|的不能通过游标更新数据|  
|**adLockBatchOptimistic**|-批处理更新<br />-允许断开连接的方案<br />-其他用户能够访问数据|由多个用户可以在一次更改数据|  
|**adLockPessimistic**|其他用户锁定时不能更改数据|-防止其他用户访问数据，同时锁定|  
|**adLockOptimistic**|-其他用户能够访问数据|由多个用户可以在一次更改数据|
