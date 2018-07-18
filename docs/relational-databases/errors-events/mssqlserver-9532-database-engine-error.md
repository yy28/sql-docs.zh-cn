---
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e779b0f514ed6892d345c2f72ecf37b8711257e3
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34329618"
---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
列集是一种非类型化的 XML 表示形式，它将表的某些列组合成为结构化的输出。 通过 XML 列集插入或更新稀疏列值时，插入到基础稀疏列的值将从 **xml** 数据类型隐式转换为另一种类型。 所提供的值无法转换为列的数据类型。  
  
## <a name="user-action"></a>用户操作  
由于无法对提供的值进行隐式转换，因此该值可能是一个无效项。 更正该错误，然后重试。 如果该值正确，修改该语句以使用单个列而不使用列集。 通过此操作可将该值显式转换为正确的数据类型。  
  
