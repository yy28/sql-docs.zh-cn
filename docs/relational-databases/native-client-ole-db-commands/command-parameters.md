---
title: 命令参数 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- parameters [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, parameters
- SQL Server Native Client OLE DB provider, commands
- parameters [SQL Server Native Client], OLE DB
- commands [OLE DB]
ms.assetid: 072ead49-ebaf-41eb-9a0f-613e9d990f26
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5db24ee3b68d1a8989200479a3ce4018e63a5177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304503"
---
# <a name="command-parameters"></a>命令参数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在命令文本中参数用问号字符标记。 例如，以下 SQL 语句标记了单个输入参数：  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 为了通过减少网络流量来提高性能，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序不会自动派生参数信息，除非在执行命令之前调用**ICommand 与参数：：获取参数信息**或**ICommandPrepare：:P重新数据。** 这意味着[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序不会自动：  
  
-   验证使用 ICommandWithParameters::SetParameterInfo 指定的数据类型的正确性****。  
  
-   将取值函数绑定信息中指定的 DBTYPE 映射到参数的正确 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 如果这两个方法指定的数据类型与参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不兼容，那么应用程序在使用该方法时将可能收到错误或产生精度损失。  
  
 若要确保不发生这种情况，应用程序应当：  
  
-   如果硬编码 ICommandWithParameters::SetParameterInfo，则应确保 pwszDataSourceType 与参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型匹配******。  
  
-   如果硬编码取值函数，则应确保绑定到参数的 DBTYPE 值与参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型具有相同类型。  
  
-   对应用程序进行编码以调用 ICommandWithParameters::GetParameterInfo，以便访问接口可以动态获取参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型****。 请注意，这会导致与服务器之间额外的网络往返。  
  
> [!NOTE]  
>  对于包含 FROM 子句的任意 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UPDATE 或 DELETE 语句，对于依赖于包含参数的子查询的任意 SQL 语句，对于在比较和类似表达式中包含参数标记或包含限定谓词的 SQL 语句，或其参数之一为函数参数的查询，访问接口不支持调用 ICommandWithParameters::GetParameterInfo****。 在对 SQL 语句进行批处理时，对于批处理中第一个语句后的语句中的参数标记，访问接口也不支持调用 ICommandWithParameters::GetParameterInfo****。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令中不允许使用注释 (/* \*/)。  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序支持 SQL 语句命令中的输入参数。 在过程调用命令上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序支持输入、输出和输入/输出参数。 输出参数值在运行时（仅当没有行集返回时）或当应用程序用尽返回的所有行集时，返回到应用程序。 若要确保返回值有效，可使用 IMultipleResults 强制使用行集****。  
  
 在 DBPARAMBINDINFO 结构中无需指定存储过程参数的名称。 对*pwszName*成员的值使用 NULL 以指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序应忽略参数名称，并且仅使用 ICommand 与参数的*rgParamOrdinals*成员中指定的表位 **：：set参数信息**。 如果命令文本中既包含命名参数又包含未命名参数，则必须在所有命名参数之前指定所有未命名参数。  
  
 如果指定了存储过程参数的名称，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将检查该名称以确保其有效。 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序在从使用者收到错误的参数名称时返回错误。  
  
> [!NOTE]  
>  为了公开对[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和用户定义类型 （UDT）[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的支持，本机客户端 OLE DB 提供程序实现了一个新的[ISSCommand 与参数接口](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)。  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
