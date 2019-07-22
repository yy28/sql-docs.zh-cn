---
title: MSSQLSERVER_5515 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: 92cdf8d0cccebbdbf0f3c4fdf6b0bacbf41f6e47
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903938"
---
# <a name="mssqlserver5515"></a>MSSQLSERVER_5515
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|5515|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|FS_OPEN_CONTAINER_FAILED|  
|消息正文|无法打开 FILESTREAM 文件的容器目录“%.*ls”。 操作系统返回 Windows 状态代码 0x%x。|  
  
## <a name="explanation"></a>解释  
无法打开为 FILESTREAM 文件指定的容器目录。  
  
## <a name="user-action"></a>用户操作  
请查看具体的 Windows 状态代码以了解错误原因。  
  
