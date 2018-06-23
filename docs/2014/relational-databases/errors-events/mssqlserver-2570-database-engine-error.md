---
title: MSSQLSERVER_2570 | Microsoft Docs
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
- 2570 (Database Engine error)
ms.assetid: 29800aa9-81aa-4371-992c-487dbb617f46
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 24f1742fd8882aa95e525d4344d1b1c1163143b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125861"
---
# <a name="mssqlserver2570"></a>MSSQLSERVER_2570
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2570|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_COLUMN_VALUE_OUT_OF_RANGE|  
|消息正文|页 P_ID，槽 S_ID 位于对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID (类型为 "TYPE")中。 列 "COLUMN_NAME" 的值超出了数据类型 "DATATYPE" 的范围。 请将该列更新为合法的值。|  
  
## <a name="explanation"></a>解释  
 指定列中包含的列值超出了列数据类型可能的值范围。  
  
## <a name="user-action"></a>用户操作  
 该错误不可修复。 将该列更新为列的数据类型范围内的值并再次运行该命令。  有关详细信息，请参阅此知识库文章 [923247](http://support.microsoft.com/kb/923247)。  
  
## <a name="see-also"></a>请参阅  
 [UPDATE (Transact-SQL)](/sql/t-sql/queries/update-transact-sql)   
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
