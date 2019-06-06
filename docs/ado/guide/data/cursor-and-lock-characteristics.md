---
title: 游标和锁定特征 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3a206a21cf7c6680a656c89c48b8f52d1069d78
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702113"
---
# <a name="cursor-and-lock-characteristics"></a>游标和锁定特征
游标的特征取决于提供程序的功能，而以下优点和缺点通常适用于各种类型的游标和锁定。  
  
|游标或锁类型|优点|缺点|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-较低的资源要求|-不能向后滚动<br />-无数据并发|  
|**adOpenStatic**|-   Scrollable|-无数据并发|  
|**adOpenKeyset**|-某些数据并发<br />-   Scrollable|较高资源要求<br />的在离线场景中不可用|  
|**adOpenDynamic**|-较高的数据并发<br />-   Scrollable|-最高资源要求<br />的在离线场景中不可用|  
|**adLockReadOnly**|-较低的资源要求<br />的高度可缩放|数据不能通过游标更新|  
|**adLockBatchOptimistic**|-Batch 更新<br />-允许断开连接的场景<br />-其他用户能够访问数据|的由多个用户可以在一次更改数据|  
|**adLockPessimistic**|数据不能更改由其他用户锁定时|-阻止其他用户访问数据时锁定|  
|**adLockOptimistic**|-其他用户能够访问数据|的由多个用户可以在一次更改数据|
