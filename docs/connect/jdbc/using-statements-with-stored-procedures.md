---
title: 结合使用语句和存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2c5cec3ba96a9ce4b96ae3b4dd92299e361902b5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923971"
---
# <a name="using-statements-with-stored-procedures"></a>结合使用语句和存储过程

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

存储过程是一个数据库过程，类似于其他编程语言中的过程，它包含于数据库本身。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]，或使用公共语言运行时 (CLR) 和某种 Visual Studio 编程语言（如 Visual Basic 或 C#），可以创建存储过程。 通常，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程可执行下列操作：  
  
- 接受输入参数并以输出参数的格式向调用过程或批处理返回多个值。  
  
- 包含用于在数据库中执行操作（包括调用其他过程）的编程语句。  
  
- 向调用过程或批处理返回状态值，以指明成功或失败（以及失败的原因）。  
  
> [!NOTE]  
> 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“了解存储过程”。  
  
为了使用存储过程来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供了 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类。 要使用那个类取决于存储过程是否需要 IN（输入）或 OUT（输出）参数。 如果存储过程不需要 IN 和 OUT 参数，则可以使用 SQLServerStatement 类；如果要多次调用存储过程或仅需要 IN 参数，则可以使用 SQLServerPreparedStatement 类。 如果存储过程同时需要 IN 和 OUT 参数，则应使用 SQLServerCallableStatement 类。 只有在存储过程仅需要 OUT 参数时，才应使用 SQLServerCallableStatement 类。  
  
> [!NOTE]  
> 存储过程还可以返回更新计数和多个结果集。 有关详细信息，请参阅[使用带有更新计数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)和[使用多个结果集](../../connect/jdbc/using-multiple-result-sets.md)。  
  
使用 JDBC 驱动程序调用带参数的存储过程时，必须结合 `call`SQLServerConnection[ 类的 ](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)prepareCall[ 方法使用 ](../../connect/jdbc/reference/sqlserverconnection-class.md) SQL 转义序列。 `call` 转义序列的完整语法如下：  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
> 有关`call` 和其他 SQL 转义序列的详细信息，请参阅[使用 SQL 转义序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
本部分中的主题说明使用 JDBC 驱动程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 转义序列调用 `call` 存储过程的可用方法。  
  
## <a name="in-this-section"></a>在本节中  
  
|主题|说明|  
|-----------|-----------------|  
|[使用不含参数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|说明如何使用 JDBC 驱动程序运行不包含输入或输出参数的存储过程。|  
|[使用含输入参数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|说明如何使用 JDBC 驱动程序运行包含输入参数的存储过程。|  
|[使用含输出参数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|说明如何使用 JDBC 驱动程序运行包含输出参数的存储过程。|  
|[使用含返回状态的存储过程](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|说明如何使用 JDBC 驱动程序运行包含返回状态值的存储过程。|  
|[使用含更新计数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|说明如何使用 JDBC 驱动程序运行返回更新计数的存储过程。|  
  
## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
