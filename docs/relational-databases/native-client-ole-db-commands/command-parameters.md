---
title: "命令参数 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-commands
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- parameters [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, parameters
- SQL Server Native Client OLE DB provider, commands
- parameters [SQL Server Native Client], OLE DB
- commands [OLE DB]
ms.assetid: 072ead49-ebaf-41eb-9a0f-613e9d990f26
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 511838c2d36c3548f99963e32b395961ea1b19e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="command-parameters"></a>命令参数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在命令文本中参数用问号字符标记。 例如，以下 SQL 语句标记了单个输入参数：  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 若要通过减少网络流量，提高性能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序不自动是派生参数信息除非**ICommandWithParameters::GetParameterInfo**或**ICommandPrepare::Prepare**执行命令前调用此方法。 这意味着， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不会自动：  
  
-   验证与指定的数据类型的正确性**ICommandWithParameters::SetParameterInfo**。  
  
-   将取值函数绑定信息中指定的 DBTYPE 映射到参数的正确 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 如果这两个方法指定的数据类型与参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不兼容，那么应用程序在使用该方法时将可能收到错误或产生精度损失。  
  
 若要确保不发生这种情况，应用程序应当：  
  
-   确保*pwszDataSourceType*匹配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]硬编码，数据将类型参数**ICommandWithParameters::SetParameterInfo**。  
  
-   如果硬编码取值函数，则应确保绑定到参数的 DBTYPE 值与参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型具有相同类型。  
  
-   要调用的应用程序的代码**ICommandWithParameters::GetParameterInfo**以便提供程序可以获取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的参数数据类型动态。 请注意，这会导致与服务器之间额外的网络往返。  
  
> [!NOTE]  
>  提供程序不支持调用**ICommandWithParameters::GetParameterInfo**任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UPDATE 或 DELETE 语句包含 FROM 子句; 具体取决于子查询包含参数; 任何 SQL 语句对于类似，包含的比较，这两个表达式中的参数标记或全称量词化谓词; 的 SQL 语句或其中的参数之一是函数的参数的查询。 当处理一批 SQL 语句时，该提供程序也不支持调用**ICommandWithParameters::GetParameterInfo**批处理中的第一个语句之后的语句中的参数标记。 注释 (/ * \*/) 中不允许[!INCLUDE[tsql](../../includes/tsql-md.md)]命令。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持在 SQL 语句命令中的输入的参数。 过程调用命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序支持输入、 输出和输入/输出参数。 输出参数值在运行时（仅当没有行集返回时）或当应用程序用尽返回的所有行集时，返回到应用程序。 若要确保返回的值是有效的使用**IMultipleResults**强制行集消耗。  
  
 在 DBPARAMBINDINFO 结构中无需指定存储过程参数的名称。 使用 NULL 值的*pwszName*成员，则指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序应忽略参数名和使用仅在指定的序号*rgParamOrdinals*的成员**ICommandWithParameters::SetParameterInfo**。 如果命令文本中既包含命名参数又包含未命名参数，则必须在所有命名参数之前指定所有未命名参数。  
  
 如果指定的存储的过程参数的名称，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序会检查以确保它是有效的名称。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序在从使用者接收错误参数名称时，返回错误。  
  
> [!NOTE]  
>  若要公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序实现一个新[ISSCommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)接口。  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
