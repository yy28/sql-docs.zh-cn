---
title: 映射数据类型 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 692f9cf66bdafecd85c693635b145749f4e432ff
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408186"
---
# <a name="mapping-data-types-odbc"></a>映射数据类型 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL 数据类型为 ODBC SQL 数据类型。 以下部分讨论 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 数据类型以及它们映射到的 ODBC SQL 数据类型。 此外，还讨论 ODBC SQL 数据类型和它们对应的 ODBC C 数据类型，以及支持的和默认的转换。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**时间戳**数据类型映射到 SQL_BINARY 或 SQL_VARBINARY ODBC 数据类型，因为中的值**时间戳**列不是**datetime**值，但**binary(8)** 或**varbinary(8)** 值，用于指示的序列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]行上的活动。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序遇到字节数为奇数的 SQL_C_WCHAR (Unicode) 值，则将截断尾随奇数字节。  
  
## <a name="dealing-with-sqlvariant-data-type-in-odbc"></a>在 ODBC 中处理 sql_variant 数据类型  
 **Sql_variant**数据类型列可以包含任何中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除大型对象 (Lob)，如**文本**， **ntext**，和**映像**。 例如，列可能包含**smallint**某些行的值**float**其他行的值并**char/nchar**的其余部分中的值。  
  
 **Sql_variant**数据类型是类似于**变体**Microsoft Visual Basic® 中的数据类型。  
  
### <a name="retrieving-data-from-the-server"></a>从服务器检索数据  
 ODBC 没有变量类型的一个概念限制的使用**sql_variant** ODBC 驱动程序中使用的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果指定了绑定， **sql_variant**数据类型必须绑定到有案可稽的 ODBC 数据类型之一。 **SQL_CA_SS_VARIANT_TYPE**，新的属性特定于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序返回的实例中的数据类型**sql_variant**给用户的列。  
  
 如果未不指定任何绑定， [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)函数可以用于确定实例中的数据类型**sql_variant**列。  
  
 若要检索**sql_variant**数据按照这些步骤操作。  
  
1.  调用**SQLFetch**要定位到检索的行。  
  
2.  调用**SQLGetData**，指定 SQL_C_BINARY 的类型和数据长度为 0。 这会强制驱动程序读取**sql_variant**标头。 标头提供该实例中的数据类型**sql_variant**列。 **SQLGetData**返回值的大小 （以字节为单位）。  
  
3.  调用[SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)通过指定**SQL_CA_SS_VARIANT_TYPE**作为其属性值。 此函数将返回的实例中的 C 数据类型**sql_variant**到客户端的列。  
  
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
  
 如果用户创建绑定使用[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)，驱动程序读取的元数据和数据。 然后，驱动程序将这些数据转换为在绑定中指定的适当 ODBC 类型。  
  
### <a name="sending-data-to-the-server"></a>将数据发送到服务器  
 **SQL_SS_VARIANT**、 新数据类型特定于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，用于数据发送到**sql_variant**列。 使用参数向服务器发送数据时 (例如，INSERT INTO TableName VALUES (？，？))， [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)用于指定的参数信息，包括 C 类型和相应[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序会将 C 数据类型转换为相应之一**sql_variant**子类型。  
  
## <a name="see-also"></a>请参阅  
 [处理结果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
