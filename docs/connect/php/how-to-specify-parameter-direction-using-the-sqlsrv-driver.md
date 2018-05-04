---
title: 如何： 使用 SQLSRV 驱动程序指定参数方向 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b2c5928dfa5d6fac8246f0dfd5ba817a3ab0416
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驱动程序指定参数方向
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题介绍如何在调用存储过程时使用 SQLSRV 驱动程序指定参数方向。 参数方向在构造传递给参数数组 （步骤 3） 时指定[sqlsrv_query](../../connect/php/sqlsrv-query.md)或[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)。  
  
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
    > 已初始化或更新为 **null**、 **DateTime**的变量或流类型无法用作输出参数。  
  
3.  使用步骤 2 中的 PHP 变量创建或更新对应，按顺序中的 TRANSACT-SQL 字符串的参数占位符的参数值的数组。 在该数组中指定每个参数的方向。 在两种方式之一中确定的每个参数的方向： 默认情况下 （对于输入参数） 或通过使用**SQLSRV_PARAM_\*** 常量 （用于输出和双向参数）。 例如，以下代码将 *$employeeId* 参数指定为输入参数，并将 *$usedVacationHours* 参数指定为双向参数：  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    为了解在一般情况下指定参数方向的语法，假定 *$var1*、 *$var2*和 *$var3* 分别对应输入、输出和双向参数。 可以使用以下方法之一来指定参数方向：  
  
    -   隐式指定输入的参数、 显式指定输出参数和显式指定双向参数：  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   显式指定输入的参数、 显式指定输出参数和显式指定双向参数：  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  执行查询中的使用[sqlsrv_query](../../connect/php/sqlsrv-query.md)或[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)和[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)。 例如，以下代码使用连接 *$conn* 执行查询 *$tsql* ，其参数值在 *$params*中指定：  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>另请参阅  
[如何：使用 SQLSRV 驱动程序检索输出参数](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
