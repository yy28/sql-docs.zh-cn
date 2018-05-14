---
title: MSSQLSERVER_5515 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
robots: noindex,nofollow
ms.openlocfilehash: f3da12118485c8aa64a493529914cd83094695b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
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
  
