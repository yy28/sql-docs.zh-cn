---
title: 操作指南：使用 SQLSRV 驱动程序指定参数方向
description: 了解如何在使用 Microsoft SQLSRV Driver for PHP for SQL Server 调用存储过程时指定参数方向
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f085fc40ded15310b81d6a447f30676ed011e7f8
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680232"
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驱动程序指定参数方向
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题介绍如何在调用存储过程时使用 SQLSRV 驱动程序指定参数方向。 参数方向是在你构造传递到 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 的参数数组（第 3 步）时指定的。  
  
### <a name="to-specify-parameter-direction"></a>指定参数方向  
  
1.  定义调用存储过程的 Transact-SQL 查询。 使用问号 (?)，而不使用要传递到存储过程的参数。 例如，此字符串将调用接受两个参数的存储过程 (UpdateVacationHours)：  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > 建议使用规范语法来调用存储过程。 有关规范语法的详细信息，请参阅[调用存储过程](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)。  
  
2.  初始化或更新对应于 Transact-SQL 查询中的占位符的 PHP 变量。 例如，以下代码将初始化 UpdateVacationHours 存储过程的两个参数：  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    >  无法将已初始化或更新为 **null**、 **DateTime**或流类型的变量用作输出参数。  
  
3.  使用第 2 步中的 PHP 变量创建或更新参数值数组，这些参数值按顺序对应于 Transact-SQL 字符串中的参数占位符。 在该数组中指定每个参数的方向。 每个参数的方向确定方法为以下两种方法之一：默认方法（用于输入参数），或使用 SQLSRV_PARAM_\***** 常数（用于输出和双向参数）。 例如，以下代码将 *$employeeId* 参数指定为输入参数，并将 *$usedVacationHours* 参数指定为双向参数：  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    为了解在一般情况下指定参数方向的语法，假定 *$var1*、 *$var2*和 *$var3* 分别对应输入、输出和双向参数。 可以使用以下方法之一来指定参数方向：  
  
    -   隐式指定输入参数，显式指定输出参数，并显式指定双向参数：  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   显式指定输入参数，显式指定输出参数，并显式指定双向参数：  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  使用 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 或使用 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 和 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) 执行查询。 例如，以下代码使用连接 *$conn* 执行查询 *$tsql* ，其参数值在 *$params*中指定：  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>另请参阅  
[如何：使用 SQLSRV 驱动程序检索输出参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[如何：使用 SQLSRV 驱动程序检索输入和输出参数](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
