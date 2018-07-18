---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9b8713cf33b75022f5b3f84fbd4fd0f2d6c96d18
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411616"
---
# <a name="mssqlserver17132"></a>MSSQLSERVER_17132
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17132|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_NODESSPACE|  
|消息正文|由于没有足够的内存可用于描述符，导致服务器启动失败。 请减少不重要的内存负载或增加系统内存。|  
  
## <a name="explanation"></a>解释  
 无法分配足够的内存来存储服务器内部描述符。  
  
## <a name="user-action"></a>用户操作  
 在计算机中添加更多内存。 一般内存故障排除步骤可能会非常有用。  
  
  
