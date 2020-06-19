---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 261d352084e490fb7f9216e1a7e352542e85a6f2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969397"
---
# <a name="mssqlserver_1807"></a>MSSQLSERVER_1807
    
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
  
  
