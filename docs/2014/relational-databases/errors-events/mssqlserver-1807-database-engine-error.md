---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a9df8969a0dbae5dbdb2959c621f287d08c9f75
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420696"
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1807|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|CANNOT_EX_LOCK|  
|消息正文|无法获得数据库 '%.*ls' 上的排他锁。 请稍后重试该操作。|  
  
## <a name="explanation"></a>解释  
 需要对数据库进行排他访问的操作无法获取它。  
  
## <a name="user-action"></a>用户操作  
 断开与该数据库的所有连接，或者稍后重试查询。  
  
  
