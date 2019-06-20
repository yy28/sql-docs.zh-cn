---
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc46a5cf1252df209243623a63ec9bdc68e71873
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867952"
---
# <a name="mssqlserver360"></a>MSSQLSERVER_360
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|360|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DML_UPDATE_SPARSE_AND_COLSET|  
|消息正文|INSERT、UPDATE 或 MERGE 语句的目标列列表不能同时包含稀疏列和包含稀疏列的列集。 请重写该语句以包括稀疏列或列集，但不能同时包括这两者。|  
  
## <a name="explanation"></a>解释  
 列集是一种非类型化的 XML 表示形式，它将表的某些列组合成为结构化的输出。 由于尝试修改列集和此列集中包含的某个列，导致这二者引用相同的列。  
  
## <a name="user-action"></a>用户操作  
 重写该语句以使其包含对列或列集的引用，但不同时包含对这二者的引用。  
  
  
