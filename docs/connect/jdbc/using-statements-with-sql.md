---
title: 使用 SQL 语句 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac74ec1c202341d6de099d97e2b7c719c2f72d27
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851862"
---
# <a name="using-statements-with-sql"></a>使用 SQL 语句
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用数据库[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]和内联 SQL 语句，有你可以使用的不同类。 使用哪个类取决于要运行的 SQL 语句的类型。  
  
 如果你的 SQL 语句中包含没有 IN 参数，使用[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类，但如果它包含在参数中，使用[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类。  
  
> [!NOTE]  
>  如果你需要使用 SQL 语句包含两个 IN，OUT 参数，必须实现它们为存储的过程和使用调用[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。 有关使用存储的过程的详细信息，请参阅[与存储过程的 Using 语句](../../connect/jdbc/using-statements-with-stored-procedures.md)。  
  
 以下各节描述了使用中的数据的不同方案[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过使用 SQL 语句的数据库。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[使用不带参数的 SQL 语句](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|说明如何使用不包含参数的 SQL 语句。|  
|[使用带参数的 SQL 语句](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|说明如何使用包含参数的 SQL 语句。|  
|[使用 SQL 语句修改数据库对象](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|说明如何使用 SQL 语句修改数据库对象。|  
|[使用 SQL 语句修改数据](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|说明如何使用 SQL 语句修改数据库中的数据。|  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序使用语句](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
