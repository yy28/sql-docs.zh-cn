---
title: 调用本机编译存储过程的最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 5439f539e126a64cff92065e049da359e89345b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127709"
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
  
 可通过 XEvent `hekaton_slow_parameter_passing` 及 `reason=named_parameters` 检测使用了（低效）命名参数的本机编译存储过程。  
  
 同样，你可以检测通过相同的 XEvent 不匹配类型的使用`hekaton_slow_parameter_passing`，与`reason=parameter_conversion`。  
  
 因为在使用内存优化表时需要实现重试逻辑（在许多情况下），并且，因为需要解决某些功能限制，所以，您可能需要创建包装解释的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。 有关示例，请参阅[内存优化表上的事务的重试逻辑的准则](memory-optimized-tables.md)。  
  
## <a name="see-also"></a>请参阅  
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  