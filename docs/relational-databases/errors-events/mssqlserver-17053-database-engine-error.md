---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d078557186af534f1f489e8fee2e0f803c548f58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100431"
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
|消息正文|%ls:遇到操作系统错误 %ls。|  
  
## <a name="explanation"></a>解释  
出现了一般性的操作系统错误。  不清楚会出现什么状态。  
  
## <a name="user-action"></a>用户操作  
此错误通常伴随某个其他错误一起出现，应参考此错误以帮助诊断该故障。 示例包括数据或日志文件读取或写入失败、注册表读取/写入操作或其他意外 Win32API 故障。  
  
