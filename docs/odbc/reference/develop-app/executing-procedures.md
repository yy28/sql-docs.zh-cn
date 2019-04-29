---
title: 执行过程 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff234d1d8e099611c8718eac5ae3b584e926a2bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061965"
---
# <a name="executing-procedures"></a>执行过程
ODBC 定义用于执行过程的标准转义序列。 此序列，并使用它的代码示例的语法，请参阅[过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 若要执行过程时，应用程序，请执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，在本部分中更高版本。  
  
2.  调用**SQLExecDirect**并将其传递一个包含执行该过程的 SQL 语句的字符串。 此语句可以使用 ODBC 或特定于 DBMS 的语法; 定义的转义序列使用特定于 DBMS 的语法的语句不是可互操作。  
  
3.  当**SQLExecDirect**调用时，该驱动程序：  
  
    -   检索当前的参数值，并根据需要将其转换。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，在本部分中更高版本。  
  
    -   数据源中调用的过程，并将其发送的已转换的参数值。 该驱动程序如何调用该过程是特定于驱动程序。 例如，可能会修改 SQL 语句，以使用数据源的 SQL 语法并提交此语句的执行，或者它可能会调用直接使用的 DBMS 数据流协议中定义的远程过程调用 (RPC) 机制的过程。  
  
    -   返回的任何输入/输出或输出参数的值或过程返回值，假定该过程成功。 处理所有其他结果 （行计数和结果集） 生成的该过程后，这些值可能不可用之前。 如果该过程失败，该驱动程序返回任何错误。
