---
title: 执行过程 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d61929c1d2afb756be5157f3378ff0fe6b4d7e95
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="executing-procedures"></a>执行过程
ODBC 定义执行过程的标准转义序列。 此序列和的代码示例，使用它的语法，请参阅[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 若要执行某个过程，应用程序，请执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，本部分中更高版本。  
  
2.  调用**SQLExecDirect**并将其传递包含执行该过程的 SQL 语句的字符串。 此语句可以使用 ODBC 或特定于 DBMS 的语法; 定义的转义序列使用特定于 DBMS 的语法的语句不是可互操作的。  
  
3.  当**SQLExecDirect**调用时，该驱动程序：  
  
    -   检索当前参数值，并根据需要转换这些。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，本部分中更高版本。  
  
    -   数据源中调用的过程，并将其发送已转换的参数值。 如何驱动程序调用该过程是特定于驱动程序。 例如，它可能会修改 SQL 语句以使用数据源的 SQL 语法并提交此语句的执行，或者它可能调用直接使用远程过程调用 (RPC) 机制在 DBMS 数据流协议中定义的过程。  
  
    -   返回的任何输入/输出或输出参数的值或过程返回值，假定该过程成功。 在处理完所有其他结果 （行计数和结果集） 生成过程后，这些值可能不可用之前。 如果过程失败，该驱动程序将返回任何错误。
