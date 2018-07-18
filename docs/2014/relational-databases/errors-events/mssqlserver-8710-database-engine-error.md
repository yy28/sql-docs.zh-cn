---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5e484ad03915e46aeac1cf0eb067cb49bc16f8c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411286"
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|8710|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|消息正文|必须提供与 CUBE、ROLLUP 或 GROUPING SET 查询一起使用的聚合函数，才能合并子聚合。 若要修复此问题，请删除该聚合函数或在 GROUP BY 子句基础上使用 UNION ALL 编写查询。|  
  
## <a name="explanation"></a>解释  
 CUBE、ROLLUP 或 GROUPING SETS 不提供合并子聚合的方法，而将它们与聚合函数一起使用即可合并子聚合。  
  
## <a name="user-action"></a>用户操作  
 若要修复此问题，请删除该聚合函数或在 GROUP BY 子句基础上使用 UNION ALL 编写查询。  
  
  
