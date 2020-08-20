---
description: MSSQLSERVER_4064
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
ms.openlocfilehash: 27f5ccbad0bd1722f8c9a4fbe1d2b7cd0fd633da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471075"
---
# <a name="mssqlserver_4064"></a>MSSQLSERVER_4064
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|4064|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DB_UFAIL_FATAL|  
|消息正文|无法打开用户默认数据库。 登录失败。|  
  
## <a name="explanation"></a>说明  
由于 SQL Server 登录名的默认数据库存在问题，该登录名无法进行连接。 数据库本身无效或登录名缺少数据库的 CONNECT 权限。  
  
## <a name="user-action"></a>用户操作  
使用 ALTER LOGIN 更改登录名的默认数据库。 将 CONNECT 权限授予登录名。  
  
