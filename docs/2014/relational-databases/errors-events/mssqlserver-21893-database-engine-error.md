---
title: MSSQLSERVER_21893 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6258f36990efccf83b43e8d8ac8bd4c2397477aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914942"
---
# <a name="mssqlserver21893"></a>MSSQLSERVER_21893
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21893|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21893|  
|消息正文|订阅服务器 (%s)（属于原始发布服务器“%s”）在重定向的发布服务器“%s”中不显示为远程服务器。 运行`sp_addlinkedserver`重定向发布服务器将这些订阅服务器添加为远程服务器上。|  
  
## <a name="explanation"></a>解释  
 `sp_validate_redirected_publisher` 使用在远程服务器上的发布服务器数据库的订阅元数据表来确定其关联的订阅服务器并验证订阅服务器的 master.dbo.sysservers 中存在关联的条目。 如果任何标识的订阅服务器不存在，则会返回此错误。  
  
 该错误不被视为严重错误。 遇到该错误的代理将此错误记录为信息性消息，但不会终止，因为在新发布服务器上无法具有适当的订阅服务器条目对复制的影响很有限。 如果在 sysservers 中没有相应的订阅服务器条目，则在通过 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 执行时，某些订阅管理活动可能会失败。 但是，可以通过显式执行管理存储过程成功地执行这些相同的活动。  
  
## <a name="user-action"></a>用户操作  
 在重定向的发布服务器上为每个标识的订阅服务器运行 `sp_addlinkedserver`，以将这些订阅服务器添加为远程服务器。 然后，运行 `sp_serveroption` 以设置该服务器的订阅服务器位。  
  
  
