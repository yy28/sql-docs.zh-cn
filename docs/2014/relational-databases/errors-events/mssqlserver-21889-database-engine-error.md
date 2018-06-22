---
title: MSSQLSERVER_21889 | Microsoft Docs
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
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 13c7ae116929c0178e9a9b2e0f381574a5cbfd75
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015450"
---
# <a name="mssqlserver21889"></a>MSSQLSERVER_21889
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21889|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21889|  
|消息正文|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例“%s”不是复制发布服务器。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例“%s”（具有分发服务器“%s”）上运行 `sp_adddistributor`，以便使该实例承载发布数据库“%s”。 确保指定的登录名和密码与用于原始发布服务器的登录名和密码相同。|  
  
## <a name="explanation"></a>解释  
 为了承载发布服务器数据库，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须为复制发布服务器。 在远程服务器上，`sp_validate_redirected_publisher` 调用 `sp_helpdistributor`，以确定该服务器是否为复制发布服务器。 如果执行存储过程 `sp_helpdistributor` 时指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目标实例不是复制发布服务器，则会返回该错误。  
  
## <a name="user-action"></a>用户操作  
 在承载发布服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上执行 `sp_adddistributor`。 在运行 `sp_adddistributor` 时，指定正确的分发服务器。 使用相同的值*@password*与参数时使用`sp_adddistributor`最初在分发服务器上运行。  
  
  