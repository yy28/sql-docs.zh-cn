---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f391f46a59ad523eabab803bf1faa3090465d25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028741"
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|4064|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DB_UFAIL_FATAL|  
|消息正文|无法打开用户默认数据库。 登录失败。|  
  
## <a name="explanation"></a>解释  
由于 SQL Server 登录名的默认数据库存在问题，该登录名无法进行连接。 数据库本身无效或登录名缺少数据库的 CONNECT 权限。  
  
## <a name="user-action"></a>用户操作  
使用 ALTER LOGIN 更改登录名的默认数据库。 将 CONNECT 权限授予登录名。  
  
