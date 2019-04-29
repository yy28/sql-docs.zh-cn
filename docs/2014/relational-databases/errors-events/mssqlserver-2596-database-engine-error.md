---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 21209de55bc010c2c85285f4cbed7305c6755f4c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914364"
---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2596|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|消息正文|未处理修复语句。 该数据库不能处于只读模式。|  
  
## <a name="explanation"></a>解释  
 此消息指示数据库处于只读模式。 当数据库处于只读模式时不能进行修复。  
  
## <a name="user-action"></a>用户操作  
 使用 ALTER DATABASE 设置要读写的数据库，然后重新运行 DBCC 命令。  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
