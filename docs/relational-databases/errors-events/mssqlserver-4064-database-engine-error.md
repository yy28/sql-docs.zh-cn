---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c58d5a054999da21c3b2850e529a067df0edfb22
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34318758"
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
  
