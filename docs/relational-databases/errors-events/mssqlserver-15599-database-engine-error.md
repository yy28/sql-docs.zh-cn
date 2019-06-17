---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c51b30e8af7c075c4b84ab04311aae5961919339
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62859041"
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
  
