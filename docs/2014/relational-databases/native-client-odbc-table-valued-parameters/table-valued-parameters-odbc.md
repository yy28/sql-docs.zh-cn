---
title: 表值参数 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31ed60f10f12bbc11037a64caa50802360b919de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467297"
---
# <a name="table-valued-parameters-odbc"></a>表值参数 (ODBC)
  针对表值参数的 ODBC 支持通过在一个调用中向服务器发送多个行，支持客户端应用程序更有效地向服务器发送参数化数据。  
  
 有关表值参数在服务器上的信息，请参阅[使用表值参数&#40;数据库引擎&#41;](../tables/use-table-valued-parameters-database-engine.md)。  
  
 在 ODBC 中，向服务器发送表值参数有两种方式：  
  
-   SQLExecDirect 或 SQLExecute 称为时，所有表值参数数据都可以在内存中。 如果表值中有多个行，此数据存储在数组中。  
  
-   SQLExecDirect 或 SQLExecute 调用时，应用程序可以指定为表值参数执行数据。 这种情况下，可以成批提供表值的各行数据，或者一次提供一行数据，以降低内存要求。  
  
 第一个选项支持存储过程封装更多业务逻辑。 例如，将订单项作为表值参数传递时，单个存储过程可以封装整个订单输入事务。 由于只需与服务器往返一次，所以此选项非常有效。 或者，可以使用不同的过程分别处理订单头和订单项，这需要为客户端和服务器之间提供更多的代码和更复杂的合同。  
  
 第二种方法为涉及海量数据的大容量操作提供了有效的机制。 该方法支持应用程序将数据行流式传送到服务器，而不是先将所有数据缓存在内存中。  
  
 创建表变量时可以创建约束和主键。 约束是确保表中数据满足特定要求的一种好方法。  
  
## <a name="in-this-section"></a>本节内容  
 [ODBC 表值参数的用法](uses-of-odbc-table-valued-parameters.md)  
 说明表值参数和 ODBC 的主要用户方案。  
  
 [表值参数的 ODBC SQL 类型](odbc-sql-type-for-table-valued-parameters.md)  
 说明 SQL_SS_TABLE 类型。 这是一种新的支持表值参数的 ODBC SQL 类型。  
  
 [表值参数描述符字段](table-valued-parameter-descriptor-fields.md)  
 说明支持表值参数的描述符字段。  
  
 [表值参数构成列的描述符字段](descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 说明包含表值参数含义的描述符字段。  
  
 [表值参数诊断记录字段](table-valued-parameter-diagnostic-record-fields.md)  
 说明已添加到诊断记录中用于支持表值参数的两个诊断字段。  
  
 [影响表值参数的语句属性](statement-attributes-that-affect-table-valued-parameters.md)  
 说明支持对表值参数列寻址的新描述符标题字段。  
  
 [表值参数和列值的绑定及数据传输](binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 说明参数绑定以及如何将表值参数传递到服务器。  
  
 [准备好的语句的表值参数元数据](table-valued-parameter-metadata-for-prepared-statements.md)  
 说明应用程序如何获取准备的过程调用的元数据。  
  
 [其他表值参数的元数据](additional-table-valued-parameter-metadata.md)  
 介绍如何使用 SQLProcedureColumns、 SQLTables 和 SQLColumns 检索表值参数的元数据。  
  
 [表值参数数据转换及其他错误和警告](table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 说明如何处理表值参数列值的错误。  
  
 [跨版本兼容性](cross-version-compatibility.md)  
 说明当 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前版本的客户端或服务器使用表值参数时可能出现的冲突。  
  
 [ODBC 表值参数 API 摘要](odbc-table-valued-parameter-api-summary.md)  
 列出支持表值参数的 ODBC 函数。  
  
 [ODBC 表值参数编程示例](../../database-engine/dev-guide/odbc-table-valued-parameter-programming-examples.md)  
 说明如何执行常见任务。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 本机客户端&#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [表值参数&#40;SQL Server 本机客户端&#41;](../native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  
