---
title: 执行程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a796c615d7dfdec11a9acb90ab4b5129cf69717
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305708"
---
# <a name="executing-procedures"></a>执行过程
ODBC 定义了执行过程的标准转义序列。 有关此序列的语法和使用它的代码示例，请参阅[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 要执行过程，应用程序执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅本节后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  调用**SQLExecDirect**并传递一个字符串，其中包含执行该过程的 SQL 语句。 此语句可以使用由 ODBC 或 DBMS 特定语法定义的转义序列;使用特定于 DBMS 的语法的语句不可互操作。  
  
3.  调用**SQLExecDirect**时，驱动程序：  
  
    -   检索当前参数值并根据需要转换它们。 有关详细信息，请参阅本节后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   调用数据源中的过程，并向其发送转换后的参数值。 驱动程序如何调用该过程是特定于驱动程序的。 例如，它可能会修改 SQL 语句以使用数据源的 SQL 语法并提交此语句以执行，或者可能直接使用 DBMS 的数据流协议中定义的远程过程调用 （RPC） 机制调用该过程。  
  
    -   返回任何输入/输出或输出参数的值或过程返回值，前提是该过程成功。 这些值可能直到处理过程生成的所有其他结果（行计数和结果集）后才可用。 如果该过程失败，驱动程序将返回任何错误。
