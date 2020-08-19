---
description: MSSQLSERVER_7920
title: MSSQLSERVER_7920 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7920 (Database Engine error)
ms.assetid: d16290ea-3875-4148-8d53-057bfee00438
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 20ff446fa2ff415e096b0d380dcbda4cdceebcc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448749"
---
# <a name="mssqlserver_7920"></a>MSSQLSERVER_7920
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|7920|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_SUMMARY_ENTRIES|  
|消息正文|已在系统目录中为数据库 ID D_ID 处理 ENTRY_COUNT 项。|  
  
## <a name="explanation"></a>说明  
这是由 DBCC CHECKALLOC 以外的所有 DBCC CHECK 命令返回的信息性消息。 返回值是所检查的总行集数。  
  
## <a name="user-action"></a>用户操作  
无  
  
