---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54a5b9a70fee2e85c4057f70f22e1b38a5d39354
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62761854"
---
# <a name="mssqlserver_9004"></a>MSSQLSERVER_9004
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9004|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_CORRUPT|  
|消息正文|处理数据库 '%.*ls' 的日志时出错。  如果可能，请从备份还原。 如果没有可用备份，可能需要重新生成日志。|  
  
## <a name="explanation"></a>说明  
 在回滚、恢复或复制期间处理日志时出错。 这可能表明操作系统检测到错误，或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 检测到内部一致性错误。  
  
## <a name="user-action"></a>用户操作  
 执行以下操作之一将更正此错误：  
  
-   从备份还原。  
  
-   重新生成日志。  
  
 此外，检查系统事件和错误日志以识别系统内可能导致该错误的问题。  
  
  
