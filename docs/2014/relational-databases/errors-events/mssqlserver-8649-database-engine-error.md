---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5e265344d3e05081ebc01f5e9f7fdd240d27c7d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62912670"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8649|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|COST_TOO_HIGH|  
|消息正文|查询已取消，因为此查询的估计开销 (%d) 出了配置的阈值 %d。 请与系统管理员联系。|  
  
## <a name="explanation"></a>说明  
 查询已取消，因为此查询的估计开销超出了为 QUERY_GOVERNOR_COST_LIMIT 设置的配置阈值。  
  
## <a name="user-action"></a>用户操作  
 将 QUERY_GOVERNOR_COST_LIMIT 选项设置为更大的值。  
  
## <a name="see-also"></a>另请参阅  
 [SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)](/sql/t-sql/statements/set-query-governor-cost-limit-transact-sql)  
  
  
