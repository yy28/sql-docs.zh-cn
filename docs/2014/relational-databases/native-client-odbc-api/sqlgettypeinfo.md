---
title: SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
caps.latest.revision: 47
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e83a45cad86f882bfcb1c7cbb15f32736d694d55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126841"
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序报表结果中的其他列 USERTYPE 设置的`SQLGetTypeInfo`。 USERTYPE 报告 DB-Library 数据类型定义，这对需要将现有 DB-Library 应用程序移植到 ODBC 的开发人员很有用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将标识视为属性，而 ODBC 将它视为数据类型。 若要解决这种不匹配，`SQLGetTypeInfo`返回的数据类型： **intidentity**， **smallintidentity**， **tinyintidentity**， **decimalidentity**，和**numericidentity**。 `SQLGetTypeInfo`结果集列 AUTO_UNIQUE_VALUE 报告这些数据类型的值为 TRUE。  
  
 有关**varchar**， **nvarchar**和**varbinary**、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将继续报告 8000、 4000 和 8000 分别为 COLUMN_SIZE值，即使没有实际限制。 这是为了确保向后兼容性。  
  
 有关**xml**数据类型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序报告称 COLUMN_SIZE 来表示不限的大小的 SQL_SS_LENGTH_UNLIMITED。  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo 和表值参数  
 表值参数的表类型实际上是元类型，即用于定义其他类型的类型。 因此，它不必通过 SQLGetTypeInfo 公开。 应用程序必须使用 SQLTables，而不是 SQLGetTypeInfo，以检索与表值参数一起使用的表类型的元数据。  
  
 有关检索表值参数的元数据的详细信息，请参阅[语句特性该 Affect Table-Valued 参数](../native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>SQLGetTypeInfo 对日期和时间增强功能的支持  
 为日期/时间类型返回的值，请参阅[目录元数据](../native-client-odbc-date-time/metadata-catalog.md)。  
  
 有关更多常规信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>SQLGetTypeInfo 对大型 CLR UDT 的支持  
 `SQLGetTypeInfo` 支持大型 CLR 用户定义类型 (UDT)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLGetTypeInfo 函数](http://go.microsoft.com/fwlink/?LinkId=59356)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  