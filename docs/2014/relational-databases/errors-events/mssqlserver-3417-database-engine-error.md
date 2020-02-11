---
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 992ec1f1b50138b19e9d5d7eea47cfaf8b45fb54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62868199"
---
# <a name="mssqlserver_3417"></a>MSSQLSERVER_3417
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3417|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|REC_BADMASTER|  
|消息正文|无法恢复 master 数据库。 SQL Server 无法运行。 请利用完整备份还原 master 数据库，修复它，或者重新生成它。 有关如何重新生成 master 数据库的详细信息，请参阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>说明  
 SQL Server 无法启动 **master** 数据库。 如果无法使 **master** 或 **tempdb** 联机，则 SQL Server 无法运行。 其他错误通常在此错误之前出现。 检查错误日志以查找根本原因。  
  
## <a name="user-action"></a>用户操作  
 还原数据库备份或修复数据库。  
  
  
