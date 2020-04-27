---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 871c5961b1c878e8eaad9d536731c57e71bb40ac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915316"
---
# <a name="mssqlserver_17132"></a>MSSQLSERVER_17132
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17132|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_NODESSPACE|  
|消息正文|由于没有足够的内存可用于描述符，导致服务器启动失败。 请减少不重要的内存负载或增加系统内存。|  
  
## <a name="explanation"></a>说明  
 无法分配足够的内存来存储服务器内部描述符。  
  
## <a name="user-action"></a>用户操作  
 在计算机中添加更多内存。 一般内存故障排除步骤可能会非常有用。  
  
  
