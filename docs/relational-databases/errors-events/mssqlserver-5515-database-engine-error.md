---
description: MSSQLSERVER_5515
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
ms.openlocfilehash: aecbc4ad6ee5c3f8a0ebcf596dca0a06392acedf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470890"
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
  
