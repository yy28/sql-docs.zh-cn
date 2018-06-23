---
title: 生成脚本向导支持的对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: 5
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f102fa4366106581c5f3ec4ff141d537531dbaa4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016322"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>生成脚本向导支持的对象
  “生成和发布脚本向导”支持 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]所支持的对象的一个子集。  
  
## <a name="supported-objects"></a>支持的对象  
 下表列出“生成和发布脚本向导”支持的可发布对象。  
  
||||||  
|-|-|-|-|-|  
|应用程序角色|数据库角色|架构|用户定义聚合|视图<sup>1</sup>|  
|Assembly|DEFAULT 约束|存储过程<sup>1</sup>|用户定义数据类型|XML 架构集合|  
|CHECK 约束|全文目录|同义词|用户定义函数||  
|CLR （公共语言运行时） 存储过程<sup>1</sup>|索引|表|用户定义表||  
|CLR 用户定义函数|规则|用户<sup>2</sup>|用户定义类型||  
  
 <sup>1</sup>发布不加密。  
  
 <sup>2</sup>作为角色发布数据库中存在任何非系统用户。  
  
  