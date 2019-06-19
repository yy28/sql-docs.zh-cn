---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c8e25f71f23742de35dcc8c9629181dd20af2f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046363"
---
# <a name="mssqlserver21899"></a>MSSQLSERVER_21899
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21899|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21899|  
|消息正文|重定向发布服务器“%s”中的查询失败，该查询用于确定原始发布服务器“%s”的订阅服务器是否存在 sysserver 条目，失败时错误为“%d”，错误消息为“%s”。|  
  
## <a name="explanation"></a>解释  
在远程服务器上，**sp_validate_redirected_publisher** 查询发布服务器数据库的订阅元数据表以确定其关联的订阅服务器。 当该查询失败时，会返回错误 21899。 验证查询要求对重定向发布服务器上的发布数据库具有访问权限。 如果在对原始发布服务器调用 **sp_adddistpublisher** 时指定的登录名无权访问重定向发布服务器上的发布数据库，则会返回错误 21899。  
  
## <a name="user-action"></a>用户操作  
请检查引用的错误消息，以确定失败的原因和采取相应的更正措施  
  
