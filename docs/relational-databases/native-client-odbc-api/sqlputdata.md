---
title: SQLPutData |微软文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e063d1053d8a6e5e10a1234d33893adf27fbc3ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302338"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  当使用 SQLPutData 发送超过 65，535 字节的数据（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对于版本 4.21a）或 400 KB 的数据（对于 SQL Server 版本 6.0 及更高版本）时，以下限制适用于SQL_LONGVARCHAR（**文本**）、SQL_WLONGVARCHAR（ntext）或SQL_LONGVARBINARY（**图像**）列：**ntext**  
  
-   引用的参数可以是 INSERT 语句中*insert_value。*  
  
-   引用的参数可以是 UPDATE 语句的 SET 子句中的*表达式*。  
  
 取消一系列 SQLPutData 调用，这些调用在块中向正在运行的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务器提供数据，会导致在使用版本 6.5 或更早版本时部分更新列的值。 调用 SQLCancel 时引用**的文本****、ntext**或**图像**列设置为中间占位符值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不支持连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 版和更低版本。  
  
## <a name="diagnostics"></a>诊断  
 SQLPutData[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有一个特定于本机客户端的 SQLSTATE：  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|22026|字符串数据，长度不匹配|如果要发送的数据长度（以字节为单位）由应用程序指定，例如，SQL_LEN_DATA_AT_EXEC（n *）n大于**n*0，则应用程序通过 SQLPutData 给出的字节总数必须与指定的长度匹配。|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 和表值参数  
 当使用具有表值参数的变量行绑定时，应用程序使用 SQLPutData。 *StrLen_Or_Ind*参数指示驱动程序已准备好为表值参数数据的下一行或行收集数据，或者没有更多的行可用：  
  
-   大于 0 的值指示可以使用下一组行值。  
  
-   0 值指示已没有更多的行要发送。  
  
-   任何小于 0 的值则会出错，导致记录一个诊断记录，该记录包含 SQLState HY090 和消息“字符串或缓冲区长度无效”。  
  
 *DataPtr*参数将被忽略，但必须设置为非 NULL 值。 有关详细信息，请参阅[表值参数和列值的绑定和数据传输](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)中变量 TVP 行绑定部分。  
  
 如果*StrLen_Or_Ind*具有SQL_DEFAULT_PARAM以外的任何值或介于 0 和SQL_PARAMSET_SIZE之间的数字（即 SQLBind 参数的*列大小*参数），则这是一个错误。 此错误导致 SQLPutData 返回 SQL_ERROR：SQLSTATE=HY090，“字符串或缓冲区长度无效”。  
  
 有关表值参数的详细信息，请参阅[&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>SQLPutData 对增强的日期和时间功能的支持  
 日期/时间类型的参数值将转换，如从[C 到 SQL 的转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)中所述。  
  
 有关详细信息，请参阅[&#40;ODBC&#41;的日期和时间改进](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>SQLPutData 对大型 CLR UDT 的支持  
 **SQLPutData**支持大型 CLR 用户定义类型 （UDT）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLPutData 函数](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
