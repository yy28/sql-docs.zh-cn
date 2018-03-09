---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52017ed6cc9280cb122f84e6ef0b0e884fe5f8ed
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|15599|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|消息正文|不能对本地临时对象设置审核和权限。|  
  
## <a name="explanation"></a>解释  
为本地或全局临时对象设置审核和权限不起作用。 这些语句不会导致错误（操作将返回成功消息），但是不起作用。  
  
此行为尚未更改，但是从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，会显示此信息性消息提醒用户。  
  
## <a name="user-action"></a>用户操作  
不需要执行任何操作，但是请考虑删除尝试对本地或全局临时对象设置审核或权限的语句。  
  
