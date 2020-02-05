---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e5342755dbbe468ff075d63a272e9967ea5b986f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68137149"
---
# <a name="mssqlserver_1807"></a>MSSQLSERVER_1807
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1807|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|CANNOT_EX_LOCK|  
|消息正文|无法获得数据库 '%.*ls' 上的排他锁。 请稍后重试该操作。|  
  
## <a name="explanation"></a>说明  
需要对数据库进行排他访问的操作无法获取它。  
  
## <a name="user-action"></a>用户操作  
断开与该数据库的所有连接，或者稍后重试查询。  
  
