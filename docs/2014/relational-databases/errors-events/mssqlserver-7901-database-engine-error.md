---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fae6e55cbe7170f795aff85400da2c5cdaef780a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85032444"
---
# <a name="mssqlserver_7901"></a>MSSQLSERVER_7901
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7901|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|消息正文|未处理修复语句。 当数据库处于紧急模式下时，不支持此级别的修复。|  
  
## <a name="explanation"></a>说明  
 数据库处于紧急模式下，而且指定的修复级别不是 REPAIR_ALLOW_DATA_LOSS。 除非指定 REPAIR_ALLOW_DATA_LOSS，否则无法在紧急模式下进行修复。  
  
## <a name="user-action"></a>用户操作  
 返回命令并指定 REPAIR_ALLOW_DATA_LOSS 选项。  
  
  
