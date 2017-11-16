---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: c8aaa148bd866ef8a420048a320ec33ce524891f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17204"></a>MSSQLSERVER_17204
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17204|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBLKIO_DEVOPENFAILED|  
|消息正文|%ls: 无法打开文件号 %d 的文件 %ls。  操作系统错误: %ls。|  
  
## <a name="explanation"></a>解释  
SQL Server 由于指定错误而无法打开指定的文件。  
  
## <a name="user-action"></a>用户操作  
诊断并更正操作系统，然后重试该操作。  
  
