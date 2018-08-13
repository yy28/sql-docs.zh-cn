---
title: SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
caps.latest.revision: 49
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4e4ad819f16c8d732533ce58f62cc6b6d7c3b80f
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565537"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用 SQLPutData 发送 65,535 字节以上的数据时，以下限制适用 (对于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本 4.21 a) 或 400 KB 的 sql_longvarchar （适用于 SQL Server 版本在 6.0 及更高版本) 的数据 (**文本**)、 SQL_WLONGVARCHAR(**ntext**) 或 SQL_LONGVARBINARY (**映像**) 列：  
  
-   引用的参数可以是*insert_value* INSERT 语句中。  
  
-   引用的参数可以是*表达式*UPDATE 语句的 SET 子句中。  
  
 正在取消的一系列提供数据块的运行的服务器的 SQLPutData 调用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 6.5 或更早版本时将导致部分更新列的值。 **文本**， **ntext**，或**图像**调用 SQLCancel 时引用的列设置为中间占位符值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不支持连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版和更低版本。  
  
## <a name="diagnostics"></a>诊断  
 还有一个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLPutData 的本机客户端特定 SQLSTATE:  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|22026|字符串数据，长度不匹配|如果以字节为单位发送数据的长度已指定应用程序，例如，使用 SQL_LEN_DATA_AT_EXEC (*n*) 其中*n*大于 0，由应用程序通过给定的字节总数SQLPutData 必须匹配指定的长度。|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 和表值参数  
 使用表值参数中使用可变行绑定时，应用程序使用 SQLPutData。 *StrLen_Or_Ind*参数指示它是驱动程序以收集数据的下一步的行的表值参数数据，或没有多个行均不可用：  
  
-   大于 0 的值指示可以使用下一组行值。  
  
-   0 值指示已没有更多的行要发送。  
  
-   任何小于 0 的值则会出错，导致记录一个诊断记录，该记录包含 SQLState HY090 和消息“字符串或缓冲区长度无效”。  
  
 *DataPtr*参数将被忽略，但是必须设置为非 NULL 值。 详细信息，请参阅部分中的可变 TVP 行绑定上[绑定和 Data Transfer of Table-Valued 参数和列值](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 如果*StrLen_Or_Ind*值不是 SQL_DEFAULT_PARAM 也介于 0 到 SQL_PARAMSET_SIZE (即*ColumnSize* SQLBindParameter 参数)，则返回错误。 此错误导致 SQLPutData 返回 SQL_ERROR：SQLSTATE=HY090，“字符串或缓冲区长度无效”。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>SQLPutData 对增强的日期和时间功能的支持  
 参数值的日期/时间类型转换中所述[从 C 到 SQL 转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>SQLPutData 对大型 CLR UDT 的支持  
 **SQLPutData**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLPutData 函数](http://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
