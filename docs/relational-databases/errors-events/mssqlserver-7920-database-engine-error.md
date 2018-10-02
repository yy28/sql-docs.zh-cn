---
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
manager: craigg
ms.openlocfilehash: 97855e4cc5b0bd9e28ef2de69622291ff175cc88
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670685"
---
# <a name="mssqlserver7920"></a>MSSQLSERVER_7920
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7920|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_SUMMARY_ENTRIES|  
|消息正文|已在系统目录中为数据库 ID D_ID 处理 ENTRY_COUNT 项。|  
  
## <a name="explanation"></a>解释  
这是由 DBCC CHECKALLOC 以外的所有 DBCC CHECK 命令返回的信息性消息。 返回值是所检查的总行集数。  
  
## <a name="user-action"></a>用户操作  
None  
  
