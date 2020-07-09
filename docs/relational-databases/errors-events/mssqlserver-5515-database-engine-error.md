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
ms.openlocfilehash: a9456aed02e9e1a2566bf0281dacd07f435af44b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728368"
---
# <a name="mssqlserver_5515"></a>MSSQLSERVER_5515
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|MSSQLSERVER|  
|事件 ID|5515|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|FS_OPEN_CONTAINER_FAILED|  
|消息正文|无法打开 FILESTREAM 文件的容器目录“%.*ls”。 操作系统返回 Windows 状态代码 0x%x。|  
  
## <a name="explanation"></a>说明  
无法打开为 FILESTREAM 文件指定的容器目录。  
  
## <a name="user-action"></a>用户操作  
请查看具体的 Windows 状态代码以了解错误原因。  
  
