---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ea57e9570d16a3f656ef095cbf9fe6ddec175ab6
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323348"
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
  
