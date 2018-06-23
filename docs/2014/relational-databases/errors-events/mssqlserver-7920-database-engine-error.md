---
title: MSSQLSERVER_7920 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 7920 (Database Engine error)
ms.assetid: d16290ea-3875-4148-8d53-057bfee00438
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bcb388953f3795fb8f654107a414ca4c7587df8d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128560"
---
# <a name="mssqlserver7920"></a>MSSQLSERVER_7920
    
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
 InclusionThresholdSetting  
  
  