---
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2bbb9d4716aac7c937f1fdbfe35f5c89f7b42db3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver360"></a>MSSQLSERVER_360
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
