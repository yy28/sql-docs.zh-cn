---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 624c23bd1a916d28a942332bb7dfc737048b28bc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17053"></a>MSSQLSERVER_17053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17053|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|OS_ERROR|  
|消息正文|%ls: 遇到操作系统错误 %ls。|  
  
## <a name="explanation"></a>解释  
出现了一般性的操作系统错误。  不清楚会出现什么状态。  
  
## <a name="user-action"></a>用户操作  
此错误通常伴随某个其他错误一起出现，应参考此错误以帮助诊断该故障。 示例包括数据或日志文件读取或写入失败、注册表读取/写入操作或其他意外 Win32API 故障。  
  
