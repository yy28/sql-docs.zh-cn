---
title: MSSQLSERVER_9532 | Microsoft Docs
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
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 75b484e68f58b534391c517b69bd7bced4e79046
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018876"
---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9532|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|消息正文|在涉及列集 '%.*ls' 的查询/DML 操作中，将列 '%.\*ls' 从数据类型 '%ls' 转换为数据类型 '%ls' 时转换失败。|  
  
## <a name="explanation"></a>解释  
 列集是一种非类型化的 XML 表示形式，它将表的某些列组合成为结构化的输出。 通过 XML 列集插入或更新稀疏列值时，插入基础稀疏列的值从 `xml` 数据类型隐式转换为另一种类型。 所提供的值无法转换为列的数据类型。  
  
## <a name="user-action"></a>用户操作  
 由于无法对提供的值进行隐式转换，因此该值可能是一个无效项。 更正该错误，然后重试。 如果该值正确，修改该语句以使用单个列而不使用列集。 通过此操作可将该值显式转换为正确的数据类型。  
  
  