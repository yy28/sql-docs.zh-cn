---
description: MSSQLSERVER_2538
title: MSSQLSERVER_2538 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c4d083a389ffb80760f025cfeaa95f5f3bbac6ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456265"
---
# <a name="mssqlserver_2538"></a>MSSQLSERVER_2538
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|2538|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|消息正文|文件 FILE。 区数 = EXTENTS，已用页数 = USED_PAGES，保留页数 = RESERVED_PAGES。|  
  
## <a name="explanation"></a>说明  
此信息是 DBCC CHECKALLOC 命令输出的一部分。 此信息是指定数据库的已分配区数、已用页数和保留页数的按文件摘要。  
  
## <a name="user-action"></a>用户操作  
无  
  
