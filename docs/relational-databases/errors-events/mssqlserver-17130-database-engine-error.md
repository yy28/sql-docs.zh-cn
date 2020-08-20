---
description: MSSQLSERVER_17130
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c60cada5e0f1172c927fdb4ef5ebd8c89e719a33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499522"
---
# <a name="mssqlserver_17130"></a>MSSQLSERVER_17130
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|17130|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_NOLOCKSPACE|  
|消息正文|没有足够的内存分配给所配置的锁数。 正尝试以较小的锁哈希表启动，但这可能会影响性能。 请与数据库管理员联系，为数据库引擎的这一实例配置更多内存。|  
  
## <a name="explanation"></a>说明  
没有足够的内存来分配所需大小的锁管理器哈希表。  将尝试分配一个较小的哈希表。  
  
## <a name="user-action"></a>用户操作  
检查服务器内存配置参数（最小/最大服务器内存），然后检查内存不足情况。 为 SQL Server 提供更多的内存。  
  
