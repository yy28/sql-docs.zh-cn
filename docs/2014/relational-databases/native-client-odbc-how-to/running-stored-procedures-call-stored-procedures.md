---
title: 调用存储过程（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: rothja
ms.author: jroth
ms.openlocfilehash: 18f9e8742fb01ef0bf3b635d0bdc3fda4e428296
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048155"
---
# <a name="call-stored-procedures-odbc"></a>调用存储过程 (ODBC)
  当 SQL 语句使用 ODBC CALL 转义子句调用存储过程时，Microsoft SQL Server 驱动程序使用远程存储过程调用（RPC）机制将该过程发送到 SQL Server。 RPC 请求在 SQL Server 中跳过大多数语句分析和参数处理，因此，其速度快于使用 Transact-SQL EXECUTE 语句。  
  
 有关演示此功能的示例应用程序，请参阅使用[ODBC&#41;&#40;处理返回代码和输出参数](running-stored-procedures-process-return-codes-and-output-parameters.md)。  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>将过程作为 RPC 运行  
  
1.  构造使用 ODBC CALL 转义序列的 SQL 语句。 该语句对每个输入、输入/输出和输出参数以及过程返回值（如果有）使用参数标记：  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  为每个输入、输入/输出和输出参数以及过程返回值（如果有）调用[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) 。  
  
3.  用[SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)执行语句。  
  
> [!NOTE]  
>  如果应用程序使用 Transact-SQL EXECUTE 语法提交过程（这与 ODBC CALL 转义序列相反），SQL Server ODBC 驱动程序会将过程调用作为 SQL 语句（而非 RPC）传递给 SQL Server。 此外，如果未使用 Transact-SQL EXECUTE 语句，则不会返回输出参数。  
  
## <a name="see-also"></a>另请参阅  
 [运行存储过程操作指南主题 &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [批处理存储过程调用](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [运行存储过程](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [调用存储过程](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [过程](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
