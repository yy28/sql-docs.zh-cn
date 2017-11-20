---
title: "检索与 SQL_NUMERIC_STRUCT 数值数据 |Microsoft 文档"
description: "C/c + + 使用 ODBC 使用 SQL_NUMERIC_STRUCT，与 SQL_C_NUMERIC 来检索 SQL Server 数值数据类型。"
documentationCenter: 
authors: MightyPen
manager: jhubbard
editor: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.suite: sql
ms.technology: dbe-data-tier-apps
ms.devlang: C++
ms.topic: article
ms.custom: 
ms.tgt_pltfrm: NA
ms.workload: Inactive
ms.date: 07/13/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed79b7c006efaeb6af03a10c7421eb71d1ab69ad
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="retrieve-numeric-data-with-sqlnumericstruct"></a>检索与 SQL 的数值数据\_数值\_结构

本文介绍如何从 SQL Server ODBC 驱动程序的数值数据检索到的数字的结构。 它还介绍如何获取使用特定的精度的正确值和缩放值。

此数据类型允许应用程序直接处理数值数据。 围绕 2003 年，ODBC 3.0 引入了新的 ODBC C 数据类型，由标识**SQL\_C\_数值**。 此数据类型是自 2017 年起仍适用。

使用 C 缓冲区中具有的类型定义**SQL\_数值\_结构**。 此结构具有用于存储精度、 小数位数、 登录和的数值数据值的字段。 本身的值存储为与最左边的位置中的最低有效字节开始部分的缩放后的整数。 

文章[C 数据类型](c-data-types.md)提供详细信息的格式和使用 SQL\_数值\_结构。 通常[附录 D](appendix-d-data-types.md) ODBC 3.0 程序员的引用的讨论数据类型。


## <a name="sqlnumericstruct-overview"></a>SQL\_数值\_结构概述


SQL\_数值\_结构定义 sqltypes.h 标头文件中，如下所示：


``` C
#define SQL_MAX_NUMERIC_LEN    16
typedef struct tagSQL_NUMERIC_STRUCT
{
   SQLCHAR    precision;
   SQLSCHAR   scale;
   SQLCHAR    sign;   /* 1 if positive, 0 if negative */
   SQLCHAR    val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

            
数值结构的精度和小数位数字段永远不会用于从仅用于输出的驱动程序中对应用程序的应用程序的输入。

驱动程序使用的默认精度 （驱动程序定义） 和默认小数位数 (0) 时将数据返回到应用程序。 除非应用程序将指定的精度和小数位数的值，该驱动程序假定默认值，并将其截断的数字数据的小数部分。

## <a name="sqlnumericstruct-code-sample"></a>SQL\_数值\_结构的代码示例

此代码示例演示如何为：

- 设置精度。
- 设置合适的比例。
- 检索正确的值。 

> [!Note]
> 任何由你提供这篇文章中的代码应由使用你自己风险。 
>
> Microsoft 提供的这些代码示例"按原样"没有任何形式的保证，任何明示或默示保证，包括但不是限于适销性和/或适用于某种特定用途的默示保证。

``` C
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <ctype.h>
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

#define MAXDSN       25
#define MAXUID       25
#define MAXAUTHSTR   25
#define MAXBUFLEN   255

SQLHENV     henv   = SQL_NULL_HENV;
SQLHDBC     hdbc1  = SQL_NULL_HDBC;     
SQLHSTMT    hstmt1 = SQL_NULL_HSTMT;
SQLHDESC    hdesc  = NULL;


SQL_NUMERIC_STRUCT NumStr;

int main()
{
   RETCODE retcode;

//Change the values below as appropriate to make a successful connection.
//szDSN: DataSourceName, szUID=userid, szAuthStr: password

UCHAR szDSN[MAXDSN+1] = "sql33",szUID[MAXUID+1]="sa", szAuthStr[MAXAUTHSTR+1] = "";
SQLINTEGER strlen1;
SQLINTEGER a;
int i,sign =1;
long myvalue, divisor;
float final_val;
   
// Allocate the Environment handle. Set the Env attribute, allocate the
//connection handle, connect to the database and allocate the statement //handle.

retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);
retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION,(SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);
retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);
retcode = SQLConnect(hdbc1, szDSN,SQL_NTS,szUID,SQL_NTS,szAuthStr,SQL_NTS);
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);

// Execute the select statement. Here it is assumed that numeric_test
//table is created using the following statements:

// Create table numeric_test (col1 numeric(5,3))
//insert into numeric_test values (25.212)

retcode = SQLExecDirect(hstmt1,(UCHAR *)"select * from numeric_test",SQL_NTS);

// Use SQLBindCol to bind the NumStr to the column that is being retrieved.

retcode = SQLBindCol(hstmt1,1,SQL_C_NUMERIC,&NumStr,19,&strlen1);

// Get the application row descriptor for the statement handle using
//SQLGetStmtAttr.

retcode = SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_ROW_DESC,&hdesc, 0, NULL);

// You can either use SQLSetDescRec or SQLSetDescField when using
// SQLBindCol. However, if you prefer to call SQLGetData, you have to
// call SQLSetDescField instead of SQLSetDescRec. For more information on
// descriptors, please refer to the ODBC 3.0 Programmers reference or
// your Online documentation.

//Used when using SQLSetDescRec
//a=b=sizeof(NumStr);

// Set the datatype, precision and scale fields of the descriptor for the 
//numeric column. Otherwise the default precision (driver defined) and 
//scale (0) are returned.

// In this case, the table contains only one column, hence the second 
//parameter contains one. Zero applies to bookmark columns. Please check 
//the programmers guide for more information.

//retcode=SQLSetDescRec(hdesc,1,SQL_NUMERIC,NULL,sizeof(NumStr),5,3,&NumStr,&a,&b);

retcode = SQLSetDescField (hdesc,1,SQL_DESC_TYPE,(VOID*)SQL_C_NUMERIC,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_PRECISION,(VOID*) 5,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_SCALE,(VOID*) 3,0);
    
// Initialize the val array in the numeric structure.

memset(NumStr.val,0,16);
   
// Call SQLFetch to fetch the first record.

while((retcode =SQLFetch(hstmt1)) != SQL_NO_DATA)
  {
// Notice that the TargetType (3rd Parameter) is SQL_ARD_TYPE, which  
//forces the driver to use the Application Row Descriptor with the 
//specified scale and precision.

   retcode = SQLGetData(hstmt1, 1, SQL_ARD_TYPE, &NumStr, 19, &a); 

// Check for null indicator.

   if ( SQL_NULL_DATA == a )
   {
   printf( "The final value: NULL\n" );
   continue;
   }

// Call to convert the little endian mode data into numeric data.

   myvalue = strtohextoval();

// The returned value in the above code is scaled to the value specified
//in the scale field of the numeric structure. For example 25.212 would
//be returned as 25212. The scale in this case is 3 hence the integer 
//value needs to be divided by 1000.

   divisor = 1;
   if(NumStr.scale > 0)
     {
    for (i=0;i< NumStr.scale; i++)   
         divisor = divisor * 10;
     }
   final_val =  (float) myvalue /(float) divisor;

// Examine the sign value returned in the sign field for the numeric
//structure.
//NOTE: The ODBC 3.0 spec required drivers to return the sign as 
//1 for positive numbers and 2 for negative number. This was changed in the
//ODBC 3.5 spec to return 0 for negative instead of 2.

      if(!NumStr.sign) sign = -1;
      else sign  =1;

   final_val *= sign;
   printf("The final value: %f\n",final_val);
    }

   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA_FOUND);

   /* clean up */ 
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);
   SQLDisconnect(hdbc1);
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
   return(0);
}
```


### <a name="interim-results"></a>临时结果：


```
//  C  ==> 12 * 1    =     12
//  7  ==> 07 * 16   =    112
//  2  ==> 02 * 256  =    512
//  6  ==> 06 * 4096 =  24576
===============================
                 Sum =  25212
```


在数值结构中，val 字段为 16 个元素的字符数组。 例如，25.212 扩展到 25212，刻度为 3。 此数字将以十六进制格式为 627 c。

驱动程序返回以下各项：

- 7 c，它的等效字符 |（通过管道传递） 中的字符数组的第一个元素。
- 等效于 62，这是在第二个元素中的 b。
- 数组元素的余数包含零，因此在缓冲区中包含 | 变形 b\0。

现在，其困难在于如何构造超出此字符串数组缩放后的整数。 在字符串中的每个字符对应于两个十六进制数字，例如最小有效位 (LSD) 和最高有效位 (MSD)。 缩放后的整数值可以与 16，从 1 开始的多个生成乘以每个数字 （MSD LSD）。

实现从小 endian 模式为缩放后的整数的转换的代码。 它是由应用程序开发人员实现此功能。 下面的代码示例是只是其中之一的各种可能的方法。


``` C
long strtohextoval()
{
    long val=0,value=0;
    int i=1,last=1,current;
    int a=0,b=0;

        for(i=0;i<=15;i++)
        {
         current = (int) NumStr.val[i];
         a= current % 16; //Obtain LSD
         b= current / 16; //Obtain MSD
            
         value += last* a;   
         last = last * 16;   
         value += last* b;
         last = last * 16;   
        }
     return value;
}
```


### <a name="applies-to-versions"></a>适用于版本


有关 SQL 上述信息\_数值\_结构适用于以下的产品版本：

- Microsoft ODBC Driver for Microsoft SQL Server 3.7
- Microsoft 数据访问组件 2.1
- Microsoft 数据访问组件 2.5
- Microsoft 数据访问组件 2.6
- Microsoft 数据访问组件 2.7


## <a name="sqlcnumeric-overview"></a>SQL\_C\_数值概述


下面的示例程序演示如何使用 SQL\_C\_数值，通过将 123.45 插入到表。 在表中，列定义为数字或 decimal，其精度为 5，并使用缩放 2。

用于运行此程序的 ODBC 驱动程序必须支持 ODBC 3.0 功能。


``` C
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

void main() {

   SQLHENV    henv  = NULL;
   SQLHDBC    hdbc  = NULL;
   SQLHSTMT   hstmt = NULL;

   SQL_NUMERIC_STRUCT   NumStr;
   SQLINTEGER           cbNumStr = sizeof (NumStr);

   SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);

   /* Set the ODBC behavior version. */ 
   SQLSetEnvAttr(henv,
         SQL_ATTR_ODBC_VERSION,
         (SQLPOINTER) SQL_OV_ODBC3,
         SQL_IS_INTEGER);

   SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);

   /* Substitute your own connection information */ 
   SQLConnect(hdbc,
      (SQLCHAR *) "MyDSN", 5,
      (SQLCHAR *) "UserID", 6,
      (SQLCHAR *) "Password", 8);

   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);

   /*
      Set up the SQL_NUMERIC_STRUCT, NumStr, to hold "123.45".

      First, we need to scale 123.45 to an integer: 12345
      One way to switch the bytes is to convert 12345 to Hex:  0x3039
      Since the least significant byte will be stored starting from the
      leftmost byte, "0x3039" will be stored as "0x3930".

      The precision and scale fields are not used for input to the driver,
      only for output from the driver. The precision and scale will be set
      in the application parameter descriptor later.
   */ 

   NumStr.sign = 1;   /* 1 if positive, 2 if negative */ 

   memset (NumStr.val, 0, 16);
   NumStr.val [0] = 0x39;
   NumStr.val [1] = 0x30;

   /* SQLBindParameter needs to be called before SQLSetDescField */ 
   SQLBindParameter(hstmt,
          1,
          SQL_PARAM_INPUT,
          SQL_C_NUMERIC,
          SQL_NUMERIC,
          5,
          2,
          &NumStr,
          0,
          (SQLINTEGER *) &cbNumStr);

   /* Modify the fields in the implicit application parameter descriptor */ 
   SQLHDESC   hdesc = NULL;

   SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);
   SQLSetDescField(hdesc, 1, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_PRECISION, (SQLPOINTER) 5, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_SCALE, (SQLPOINTER) 2, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_DATA_PTR, (SQLPOINTER) &NumStr, 0);

   SQLExecDirect(hstmt,
         (SQLCHAR *) "INSERT INTO table (numeric_column) VALUES (?)",
         SQL_NTS);

   SQLFreeHandle(SQL_HANDLE_STMT, hstmt);

   SQLDisconnect (hdbc);

   SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
}
```


<!--
GeneMi historical notes, 2017/July/12. Per Jason.C

http://go.microsoft.com/fwlink/?LinkId=147596

https://support.microsoft.com/en-us/help/222831

http://web.archive.org/web/20140319133434/http:/support.microsoft.com:80/kb/222831

http://web.archive.org/web/20080505073901/http:/support.microsoft.com:80/kb/181254

https://docs.microsoft.com/en-us/sql/odbc/reference/appendixes/c-data-types
-->


