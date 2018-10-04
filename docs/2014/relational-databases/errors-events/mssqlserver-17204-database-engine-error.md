---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2fd28a126b3a0a7f833c6410d4e590b5dc07e5a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147052"
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
  
  
