---
title: 运行存储过程（OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6329b0ff8f4d502916d2046e404fcecac8fc5869
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73759344"
---
# <a name="stored-procedures---running"></a>存储过程 - 运行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  执行语句时，对数据源调用存储过程（而不是直接在客户端应用程序中执行或准备语句）可以：  
  
-   提高性能。  
  
-   降低网络开销。  
  
-   提供更好的一致性。  
  
-   提高准确性。  
  
-   增加功能。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持三种 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程用于返回数据的机制：  
  
-   过程中的每一条 SELECT 语句都生成一个结果集。  
  
-   过程可以通过输出参数返回数据。  
  
-   过程可以具有整数返回代码。  
  
 应用程序必须能够处理来自存储过程的所有这些输出。  
  
 在结果处理期间，不同的 OLE DB 访问接口返回输出参数和返回值的时间不同。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序的情况下，在使用者检索或取消存储过程返回的结果集之前，不会提供输出参数和返回代码。 返回代码和输出参数在最后一个来自服务器的 TDS 数据包中返回。  
  
 访问接口返回输出参数和返回值时，使用 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性进行报告。 此属性位于 DBPROPSET_DATASOURCEINFO 属性集中。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性设置为 DBPROPVAL_OA_ATROWRELEASE，以指示在处理或释放结果集之前，不会返回返回代码和输出参数。  
  
## <a name="see-also"></a>另请参阅  
 [存储过程](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
