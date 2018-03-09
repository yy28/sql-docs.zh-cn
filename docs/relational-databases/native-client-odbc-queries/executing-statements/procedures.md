---
title: "过程 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5f5e26d9616b6a0a15793463bc3e01f6fbd697f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="procedures"></a>过程
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  存储过程是包含一个或多个 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句的预先编译的可执行对象。 存储过程可具有输入和输出参数，并且还可以生成整数返回代码。 应用程序可以通过使用目录函数枚举可用的存储过程。  
  
 以 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 为目标的 ODBC 应用程序只应使用直接执行以调用某一存储过程。 当连接到早期版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序实现[SQLPrepare 函数](http://go.microsoft.com/fwlink/?LinkId=59360)通过创建临时存储的过程，然后称为上**SQLExecute**。 它将添加开销能够**SQLPrepare**创建临时存储的过程，只能调用目标存储过程而不是直接执行目标存储过程。 即使在连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的某一实例时，准备调用都要求额外的网络上的往返，并且生成只调用存储过程执行计划的执行计划。  
  
 在执行某一存储过程时，ODBC 应用程序应使用 ODBC CALL 语法。 驱动程序将优化，以便在使用 ODBC CALL 语法时，使用远程过程调用机制来调用该过程。 这比用于将 [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 语句发送到服务器的机制效率更高。  
  
 有关详细信息，请参阅[运行存储过程](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)。  
  
## <a name="see-also"></a>另请参阅  
 [正在执行语句 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
