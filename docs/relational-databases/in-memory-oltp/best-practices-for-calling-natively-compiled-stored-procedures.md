---
title: "调用本机编译存储过程的最佳做法 | Microsoft Docs"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2ecd5bafd4a2092ea51556b898284456d8abf2d7
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>调用本机编译存储过程的最佳做法
  本机编译存储过程：  
  
-   通常用于应用程序中性能至关重要的部分。  
  
-   频繁执行。  
  
-   操作速度快。  
  
 使用本机编译存储过程所得的性能优势随行数和该过程所处理的逻辑数的上升而增加。 例如，如果本机编译存储过程使用以下一项或多项操作，将获得更好的性能：  
  
-   聚合。  
  
-   嵌套循环联接。  
  
-   多语句选择、插入、更新和删除操作。  
  
-   复杂表达式。  
  
-   程序逻辑，如条件语句和循环。  
  
 如果只需处理一行，则使用本机编译存储过程可能没有任何性能优势。  
  
 避免服务器映射参数名称和转换类型：  
  
-   使传递给过程的参数类型与过程定义中的类型相匹配。  
  
-   在调用本机编译的存储过程时使用序数（无名称）参数。 要实现最高效的执行，请勿使用命名参数。  
  
 可通过 XEvent **natively_compiled_proc_slow_parameter_passing** 检测本机编译的存储过程的参数是否低效：
 - 不匹配的类型：**reason=parameter_conversion**
 - 命名参数：**reason=named_parameters**
 - 默认值：**reason=default** 
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  

