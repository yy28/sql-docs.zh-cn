---
description: 执行过程
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4a5f790a0e79e313924e9408f9338483931691c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499908"
---
# <a name="executing-procedures"></a>执行过程
ODBC 为执行过程定义了标准的转义序列。 有关此序列的语法以及使用它的代码示例，请参阅 [过程调用](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
 若要执行某一过程，应用程序需要执行以下操作：  
  
1.  设置任何参数的值。 有关详细信息，请参阅本部分后面的 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  调用 **SQLExecDirect** 并向其传递一个字符串，其中包含执行该过程的 SQL 语句。 此语句可以使用由 ODBC 或 DBMS 特定的语法定义的转义序列;使用 DBMS 特定语法的语句不可互操作。  
  
3.  调用 **SQLExecDirect** 时，驱动程序：  
  
    -   检索当前参数值，并根据需要对其进行转换。 有关详细信息，请参阅本部分后面的 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   调用数据源中的过程，并向其发送转换后的参数值。 驱动程序调用该过程的方式特定于驱动程序。 例如，它可能会修改 SQL 语句以使用数据源的 SQL 语法并提交此语句以执行，或者可以使用远程过程调用直接调用过程 (在 DBMS 的数据流协议中定义的 RPC) 机制。  
  
    -   返回任何输入/输出参数或过程返回值的值，前提是该过程成功。 这些值可能直到处理完所有其他结果 (行计数和过程生成) 的结果集之后才可用。 如果此过程失败，则驱动程序将返回任何错误。
