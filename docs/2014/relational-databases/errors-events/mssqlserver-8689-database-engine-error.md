---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f0853d7db0664e75140c0e5478af19c233a2517
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761713"
---
# <a name="mssqlserver_8689"></a>MSSQLSERVER_8689
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8689|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|USEPLAN_ERR_NO_DB|  
|消息正文|USE PLAN 提示中指定的数据库 '%.*ls' 不存在。 请指定一个现有数据库。|  
  
## <a name="explanation"></a>说明  
 USE PLAN 提示中指定的数据库不存在。  
  
## <a name="user-action"></a>用户操作  
 请确保在 USE PLAN 提示中指定的所有数据库均存在。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的查询提示 &#40;](/sql/t-sql/queries/hints-transact-sql-query)   
 [计划指南](../performance/plan-guides.md)  
  
  
