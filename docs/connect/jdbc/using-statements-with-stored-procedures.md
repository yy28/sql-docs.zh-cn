---
title: "使用语句与存储过程 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f617fdf969c0bdd238b07cb0def1b0a948a4d328
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-statements-with-stored-procedures"></a>使用带有存储过程的语句
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  存储过程是一个数据库过程，类似于其他编程语言中的过程，它包含于数据库本身。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，存储的过程可以通过使用创建[!INCLUDE[tsql](../../includes/tsql_md.md)]，或通过使用公共语言运行时 (CLR) 和一个 Visual Studio 编程语言，如 Visual Basic 或 C#。 通常情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]存储的过程可以执行以下操作：  
  
-   接受输入参数并以输出参数的格式向调用过程或批处理返回多个值。  
  
-   包含用于在数据库中执行操作（包括调用其他过程）的编程语句。  
  
-   向调用过程或批处理返回状态值，以指明成功或失败（以及失败的原因）。  
  
> [!NOTE]  
>  有关详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]存储的过程，请参阅"了解"存储过程中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
 若要在中处理数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用存储的过程中，数据库[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)，和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。 要使用那个类取决于存储过程是否需要 IN（输入）或 OUT（输出）参数。 如果该存储的过程要求没有 IN 或 OUT 参数，你可以使用 SQLServerStatement 类;如果存储的过程将会调用多次，或需要仅在参数中，你可以使用 SQLServerPreparedStatement 类。 如果存储的过程需要这两个在输入和输出参数，你应使用 SQLServerCallableStatement 类。 它是仅当存储的过程需要 OUT 参数，你将需要使用 SQLServerCallableStatement 类的开销。  
  
> [!NOTE]  
>  存储过程还可以返回更新计数和多个结果集。 有关详细信息，请参阅[存储过程使用更新计数](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)和[使用多个结果集](../../connect/jdbc/using-multiple-result-sets.md)。  
  
 当你使用 JDBC 驱动程序调用带参数的存储的过程时，必须使用`call`一起使用的 SQL 转义序列[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 完整语法`call`转义序列包含，如下所示：  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  有关详细信息`call`和转义序列，请参阅其他 SQL[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 此部分中的主题描述了方法，可以调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用 JDBC 驱动程序存储过程和`call`SQL 转义序列。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[不使用任何参数的存储的过程](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|说明如何使用 JDBC 驱动程序运行不包含输入或输出参数的存储过程。|  
|[使用输入参数的存储的过程](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|说明如何使用 JDBC 驱动程序运行包含输入参数的存储过程。|  
|[使用具有输出参数的存储的过程](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|说明如何使用 JDBC 驱动程序运行包含输出参数的存储过程。|  
|[使用返回的状态的存储的过程](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|说明如何使用 JDBC 驱动程序运行包含返回状态值的存储过程。|  
|[使用更新计数的存储的过程](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|说明如何使用 JDBC 驱动程序运行返回更新计数的存储过程。|  
  
## <a name="see-also"></a>另请参阅  
 [语句使用 JDBC 驱动程序](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  

