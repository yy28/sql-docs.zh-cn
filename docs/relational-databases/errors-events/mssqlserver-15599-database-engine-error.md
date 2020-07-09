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
ms.openlocfilehash: ce83bdef9b7dc694bddee8b7ec61f319cacccbb2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780954"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|15599|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|消息正文|不能对本地临时对象设置审核和权限。|  
  
## <a name="explanation"></a>说明  
为本地或全局临时对象设置审核和权限不起作用。 这些语句不会导致错误（操作将返回成功消息），但是不起作用。  
  
此行为尚未更改，但是从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，会显示此信息性消息提醒用户。  
  
## <a name="user-action"></a>用户操作  
不需要执行任何操作，但是请考虑删除尝试对本地或全局临时对象设置审核或权限的语句。  
  
