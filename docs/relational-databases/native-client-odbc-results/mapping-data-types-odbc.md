---
title: 映射数据类型 （ODBC） |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92426c854758d07a9d62ec57510d202b870dd9f2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304617"
---
# <a name="mapping-data-types-odbc"></a>映射数据类型 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将 SQL 数据类型映射到 ODBC SQL 数据类型。 以下部分讨论 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 数据类型以及它们映射到的 ODBC SQL 数据类型。 此外，还讨论 ODBC SQL 数据类型和它们对应的 ODBC C 数据类型，以及支持的和默认的转换。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**时间戳**数据类型映射到SQL_BINARY或SQL_VARBINARY ODBC 数据类型，因为**时间戳**列中的值不是**日期时间**值，而是指示行上活动序列的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**二进制（8）** 或**varbinary（8）** 值。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序遇到字节数为奇数的 SQL_C_WCHAR (Unicode) 值，则将截断尾随奇数字节。  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>在 ODBC 中处理 sql_variant 数据类型  
 **sql_variant**数据类型列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以包含除大型对象 （LOB） 以外的任何数据类型，如**文本****、ntext**和**图像**。 例如，该列可以包含某些行**的较小值**、其他行的**浮动**值和其余行中的**char/nchar**值。  
  
 **sql_variant**数据类型类似于 Microsoft 可视化基本®中的**变体**数据类型。  
  
### <a name="retrieving-data-from-the-server"></a>从服务器检索数据  
 ODBC 没有变体类型的概念，限制在 中使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sql_variant**数据类型与 ODBC 驱动程序在 。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，如果指定绑定，则**sql_variant**数据类型必须绑定到一个已记录的 ODBC 数据类型。 **SQL_CA_SS_VARIANT_TYPE**（一个特定于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序的新属性）将**sql_variant**列中实例的数据类型返回给用户。  
  
 如果未指定绑定，[则 SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)函数可用于确定**sql_variant**列中实例的数据类型。  
  
 要检索**sql_variant，** 请按照以下步骤操作。  
  
1.  调用**SQLFetch**以定位到检索的行。  
  
2.  调用**SQLGetData**，为类型指定SQL_C_BINARY，为数据长度指定 0。 这将强制驱动程序读取**sql_variant**标头。 标头在**sql_variant**列中提供该实例的数据类型。 **SQLGetData**返回值的大小（以字节为单位）。  
  
3.  通过将**SQL_CA_SS_VARIANT_TYPE**指定为其属性值来调用[SQLColAttribute。](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 此函数将**sql_variant**列中实例的 C 数据类型返回给客户端。  
  
 以下是演示上述步骤的代码片段。  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 如果用户使用[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)创建绑定，则驱动程序读取元数据和数据。 然后，驱动程序将这些数据转换为在绑定中指定的适当 ODBC 类型。  
  
### <a name="sending-data-to-the-server"></a>将数据发送到服务器  
 **SQL_SS_VARIANT**（一种特定于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序的新数据类型）用于发送到**sql_variant**列的数据。 使用参数（例如，插入表名称值（?,?））将数据发送到服务器时[，SQLBind参数](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)用于指定参数信息，包括 C 类型和相应的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型。 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序将 C 数据类型转换为适当的**sql_variant**子类型之一。  
  
## <a name="see-also"></a>另请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
