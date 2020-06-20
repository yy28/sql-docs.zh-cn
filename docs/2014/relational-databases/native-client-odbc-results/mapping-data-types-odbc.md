---
title: 映射数据类型（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a87497d52e8f011b35933c8e1cea9cd8269a4617
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039452"
---
# <a name="mapping-data-types-odbc"></a>映射数据类型 (ODBC)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 SQL 数据类型映射到 ODBC sql 数据类型。 以下部分讨论 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 数据类型以及它们映射到的 ODBC SQL 数据类型。 此外，还讨论 ODBC SQL 数据类型和它们对应的 ODBC C 数据类型，以及支持的和默认的转换。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Timestamp**数据类型映射到 SQL_BINARY 或 SQL_VARBINARY ODBC 数据类型，因为**时间戳**列中的值不是**datetime**值，而是表示行上的活动序列的**BINARY （8）** 或**VARBINARY （8）** 值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序遇到字节数为奇数的 SQL_C_WCHAR (Unicode) 值，则将截断尾随奇数字节。  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>在 ODBC 中处理 sql_variant 数据类型  
 " **Sql_variant**数据类型" 列可以包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 除大型对象（lob）以外的任何数据类型，如**text**、 **ntext**和**image**。 例如，列可能包含某些行的**smallint**值、其他行的**float**值，以及余数中的**char/nchar**值。  
  
 **Sql_variant**的数据类型类似于 Microsoft Visual Basic 中的**variant**数据类型??。  
  
### <a name="retrieving-data-from-the-server"></a>从服务器检索数据  
 ODBC 没有变体类型的概念，因此限制在中使用 ODBC 驱动程序的**sql_variant**数据类型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，如果指定了 binding，则**sql_variant**数据类型必须绑定到其中一个已记录的 ODBC 数据类型。 **SQL_CA_SS_VARIANT_TYPE**，特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序的新属性将向用户返回**sql_variant**列中的实例的数据类型。  
  
 如果未指定绑定，则可以使用[SQLGetData](../native-client-odbc-api/sqlgetdata.md)函数来确定**sql_variant**列中的实例的数据类型。  
  
 若要检索**sql_variant**数据，请执行以下步骤。  
  
1.  调用**SQLFetch**以定位到检索到的行。  
  
2.  调用**SQLGetData**，指定类型 SQL_C_BINARY，并指定0作为数据长度。 这会强制驱动程序读取**sql_variant**标头。 标头在**sql_variant**列中提供该实例的数据类型。 **SQLGetData**返回值的大小（以字节为单位）。  
  
3.  通过将**SQL_CA_SS_VARIANT_TYPE**指定为其属性值来调用[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) 。 此函数将**sql_variant**列中的实例的 C 数据类型返回到客户端。  
  
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
  
 如果用户使用[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)创建绑定，则驱动程序将读取元数据和数据。 然后，驱动程序将这些数据转换为在绑定中指定的适当 ODBC 类型。  
  
### <a name="sending-data-to-the-server"></a>将数据发送到服务器  
 **SQL_SS_VARIANT**，特定于 NATIVE Client ODBC 驱动程序的一种新数据类型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于发送到**sql_variant**列的数据。 使用参数将数据发送到服务器时（例如，INSERT INTO TableName VALUES （?,?））， [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)用于指定参数信息，包括 C 类型和相应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序会将 C 数据类型转换为相应的**sql_variant**子类型之一。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;处理结果](processing-results-odbc.md)  
  
  
