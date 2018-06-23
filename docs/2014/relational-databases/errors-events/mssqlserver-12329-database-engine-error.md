---
title: MSSQLSERVER_12329 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 01d7f8f0f7833b3ef6c5fb5c87777bb6461d3b41
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128993"
---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|12329|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|消息正文|*construct* 不支持排序规则中代码页不是 1252 的数据类型 char(n) 和 varchar(n)。|  
  
## <a name="explanation"></a>解释  
 请勿使用排序规则中代码页不是 1252 的数据类型 char(n) 和 varchar(n)。  
  
## <a name="user-action"></a>用户操作  
 可能生成此错误的一种意外情况是：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
 请改用：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  
  