---
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a217a84e7c76d54c64aca4191737aa9166464e3c
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver3417"></a>MSSQLSERVER_3417
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3417|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|REC_BADMASTER|  
|消息正文|无法恢复 master 数据库。 SQL Server 无法运行。 请利用完整备份还原 master 数据库，修复它，或者重新生成它。 有关如何重新生成 master 数据库的详细信息，请参阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>解释  
SQL Server 无法启动 **master** 数据库。 如果无法使 **master** 或 **tempdb** 联机，则 SQL Server 无法运行。 其他错误通常在此错误之前出现。 检查错误日志以查找根本原因。  
  
## <a name="user-action"></a>用户操作  
还原数据库备份或修复数据库。  
  
