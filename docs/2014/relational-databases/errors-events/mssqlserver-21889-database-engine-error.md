---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 262b2c795da92b2ef32c6956d9a2deda0e45a39d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915224"
---
# <a name="mssqlserver_21889"></a>MSSQLSERVER_21889
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21889|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21889|  
|消息正文|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例“%s”不是复制发布服务器。 在 `sp_adddistributor` 实例“%s”（具有分发服务器“%s”）上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，以便使该实例承载发布数据库“%s”。 确保指定的登录名和密码与用于原始发布服务器的登录名和密码相同。|  
  
## <a name="explanation"></a>说明  
 为了承载发布服务器数据库，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须为复制发布服务器。 在远程服务器上，`sp_validate_redirected_publisher` 调用 `sp_helpdistributor`，以确定该服务器是否为复制发布服务器。 如果执行存储过程 `sp_helpdistributor` 时指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目标实例不是复制发布服务器，则会返回该错误。  
  
## <a name="user-action"></a>用户操作  
 在承载发布服务器数据库的 `sp_adddistributor` 实例上执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在运行 `sp_adddistributor` 时，指定正确的分发服务器。 使用与最初在分发服务器*@password*上运行时`sp_adddistributor`使用的参数相同的值。  
  
  
