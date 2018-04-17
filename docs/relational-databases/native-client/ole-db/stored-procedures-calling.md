---
title: 调用存储的过程 (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [SQL Server Native Client], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: 8e5738e5-4bbe-4f34-bd69-0c0633290bdd
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 901bea0996dd993f8238df9c73301f2cc874f65e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="stored-procedures---calling"></a>存储的过程的调用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  存储过程可以有零个或多个参数。 它还可以返回值。 使用时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序，可以通过传递给存储过程的参数：  
  
-   对数据值进行硬编码。  
  
-   使用参数标记 (?) 指定参数，将程序变量绑定到参数标记，然后将数据值放在程序变量中。  
  
> [!NOTE]  
>  在使用 OLE DB 和命名参数调用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程时，参数名称必须以“@”字符开头。 这是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 特有的限制。 与 MDAC 相比，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口会更加严格地强制实施此限制。  
  
 若要支持参数， **ICommandWithParameters**接口公开命令对象上。 若要使用参数，使用者首先介绍的参数到提供程序通过调用**ICommandWithParameters::SetParameterInfo**方法 (或 （可选） 准备调用的调用语句**GetParameterInfo**方法)。 然后，使用者创建一个指定缓冲区结构的取值函数并将参数值放入该缓冲区中。 最后，它会将访问器和指针的句柄传递到的缓冲区**执行**。 在更高版本调用**执行**，使用者将新的参数值放入缓冲区和调用**执行**访问器句柄和缓冲区指针。  
  
 一个可调用使用参数的临时存储的过程的命令必须首先调用**ICommandWithParameters::SetParameterInfo**之前已成功准备命令定义参数信息。 这是因为临时存储过程的内部名称与客户端使用的外部名称不同，并且 SQLOLEDB 无法通过查询系统表来确定临时存储过程的参数信息。  
  
 以下是参数绑定过程涉及的步骤：  
  
1.  在 DBPARAMBINDINFO 结构的数组中填写参数信息，即，参数名、参数数据类型特定于访问接口的名称或者标准数据类型名称，等等。 数组中的每个结构都描述一个参数。 然后将此数组传递给**SetParameterInfo**方法。  
  
2.  调用**ICommandWithParameters::SetParameterInfo**方法，用于描述到提供程序的参数。 **SetParameterInfo**指定每个参数的本机数据类型。 **SetParameterInfo**参数是：  
  
    -   要设定其类型信息的参数的数量。  
  
    -   要设定其类型信息的参数序号的数组。  
  
    -   DBPARAMBINDINFO 结构的数组。  
  
3.  通过创建参数访问器**IAccessor::CreateAccessor**命令。 取值函数指定缓冲区的结构并将参数值放在此缓冲区中。 **CreateAccessor**命令从一组绑定创建一个访问器。 使用者使用 DBBINDING 结构数组来描述这些绑定。 每个绑定都将单个参数关联到使用者的缓冲区，并且包含诸如以下所示的信息：  
  
    -   应用绑定的参数的序号。  
  
    -   所绑定的内容（数据值、其长度以及其状态）。  
  
    -   缓冲区中到这些部分中每个部分的偏移量。  
  
    -   数据值存在于使用者的缓冲区中时的长度和类型。  
  
     取值函数通过其类型为 HACCESSOR 的句柄进行标识。 返回此句柄**CreateAccessor**方法。 每当使用者完成后使用访问器中，必须调用使用者**ReleaseAccessor**方法来释放它所包含的内存。  
  
     当使用者调用方法，如**ICommand::Execute**，它将该句柄传递给访问器和指向自身的缓冲区的指针。 访问接口使用该取值函数确定如何传送缓冲区中包含的数据。  
  
4.  填写 DBPARAMS 结构。 使用者变量值都作为从哪个输入参数和值写入到哪个输出参数传递到运行时在**ICommand::Execute** DBPARAMS 结构中。 DBPARAMS 结构包括三个元素：  
  
    -   指向缓冲区的指针，根据取值函数句柄指定的绑定，访问接口将从该缓冲区中检索输入参数数据并将输出参数数据返回到该缓冲区中。  
  
    -   缓冲区中参数组的数量。  
  
    -   在步骤 3 中创建的取值函数句柄。  
  
5.  通过使用执行命令**ICommand::Execute**。  
  
## <a name="methods-of-calling-a-stored-procedure"></a>调用存储过程的方法  
 在执行中的存储的过程时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持:  
  
-   ODBC CALL 转义序列。  
  
-   远程过程调用 (RPC) 转义序列。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 语句。  
  
### <a name="odbc-call-escape-sequence"></a>ODBC 调用转义序列  
 如果你知道参数信息，请调用**ICommandWithParameters::SetParameterInfo**方法，用于描述提供程序的参数。 否则，在使用 ODBC CALL 语法调用存储过程时，访问接口将调用一个 Helper 函数来查找存储过程的参数信息。  
  
 如果您不知道确切的参数信息（参数元数据），建议使用 ODBC CALL 语法。  
  
 使用 ODBC CALL 转义序列调用过程的常用语法是：  
  
 {[**?=**]**call***procedure_name*[**(**[*parameter*][**,**[*parameter*]]...**)**]}  
  
 例如：  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>RPC 转义序列  
 使用 RPC 转义序列调用存储过程的语法与 ODBC CALL 语法类似。 如果要多次调用过程，则在调用存储过程的三种方法中，RPC 转义序列可以提供最佳的性能。  
  
 如果使用 RPC 转义序列执行存储过程，则访问接口不会调用任何 Helper 函数来确定参数信息（使用 ODBC CALL 语法时则会调用 Helper 函数）。 RPC 语法比 ODBC CALL 语法简单，因此命令的分析速度更快，从而提高了性能。 在这种情况下，你需要通过执行提供的参数信息**ICommandWithParameters::SetParameterInfo**。  
  
 RPC 转义序列要求您具有返回值。 如果存储过程不返回值，则服务器默认返回 0。 此外，您无法对存储过程打开 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 游标。 存储的过程准备隐式调用**ICommandPrepare::Prepare**将失败。 由于无法准备 RPC 调用，你可以查询列元数据;IColumnsInfo::GetColumnInfo 和 IColumnsRowset::GetColumnsRowset 将返回 DB_E_NOTPREPARED。  
  
 如果知道所有参数元数据，建议采用 RPC 转义序列方式执行存储过程。  
  
 以下是使用 RPC 转义序列调用存储过程的一个例子：  
  
```  
{rpc SalesByCategory}  
```  
  
 有关演示 RPC 转义序列的示例应用，请参阅[执行存储过程 & #40;使用 RPC 语法 & #41;和处理返回代码和输出参数 & #40; OLE DB & #41;](../../../relational-databases/native-client-ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>Transact-SQL EXECUTE 语句  
 ODBC 调用转义序列和 RPC 转义序列是首选的方法调用存储的过程而不是[执行](../../../t-sql/language-elements/execute-transact-sql.md)语句。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用的 RPC 机制[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]以优化命令处理。 此 RPC 协议通过避免在服务器上进行大量参数处理和语句分析来提高性能。  
  
 这是一个示例的[!INCLUDE[tsql](../../../includes/tsql-md.md)]**执行**语句：  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>另请参阅  
 [存储的过程](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
