---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b63be325273e4df33d837ec1548ed46701323977
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967867"
---
# <a name="mssqlserver_17130"></a>MSSQLSERVER_17130
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
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
  
  
