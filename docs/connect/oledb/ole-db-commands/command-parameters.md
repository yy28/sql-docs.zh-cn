---
title: 命令参数 |Microsoft 文档
description: 命令参数
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, parameters
- OLE DB Driver for SQL Server, commands
- parameters [OLE DB Driver for SQL Server], OLE DB
- commands [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2d1fb6d8461f9b23842b3f94c6fb88ebbf207598
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666037"
---
# <a name="command-parameters"></a>命令参数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在命令文本中参数用问号字符标记。 例如，以下 SQL 语句标记了单个输入参数：  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 为了减少网络流量，从而提高性能，SQL Server 的 OLE DB 驱动程序并不自动派生参数信息除非**ICommandWithParameters::GetParameterInfo**或**ICommandPrepare::准备**执行命令前调用此方法。 这意味着，在 SQL Server 的 OLE DB 驱动程序不会自动：  
  
-   验证与指定的数据类型的正确性**ICommandWithParameters::SetParameterInfo**。  
  
-   将取值函数绑定信息中指定的 DBTYPE 映射到参数的正确 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。  
  
 如果这两个方法指定的数据类型与参数的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型不兼容，那么应用程序在使用该方法时将可能收到错误或产生精度损失。  
  
 若要确保不发生这种情况，应用程序应当：  
  
-   确保*pwszDataSourceType*匹配[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]硬编码，数据将类型参数**ICommandWithParameters::SetParameterInfo**。  
  
-   如果硬编码取值函数，则应确保绑定到参数的 DBTYPE 值与参数的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型具有相同类型。  
  
-   要调用的应用程序的代码**ICommandWithParameters::GetParameterInfo**以便提供程序可以获取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的参数数据类型动态。 请注意，这会导致与服务器之间额外的网络往返。  
  
> [!NOTE]  
>  提供程序不支持调用**ICommandWithParameters::GetParameterInfo**任何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]UPDATE 或 DELETE 语句包含 FROM 子句; 具体取决于子查询包含参数; 任何 SQL 语句对于类似，包含的比较，这两个表达式中的参数标记或全称量词化谓词; 的 SQL 语句或其中的参数之一是函数的参数的查询。 当处理一批 SQL 语句时，该提供程序也不支持调用**ICommandWithParameters::GetParameterInfo**批处理中的第一个语句之后的语句中的参数标记。 注释 (/ * \*/) 中不允许[!INCLUDE[tsql](../../../includes/tsql-md.md)]命令。  
  
 SQL Server 的 OLE DB 驱动程序支持在 SQL 语句命令中的输入的参数。 过程调用命令在 SQL Server 的 OLE DB 驱动程序支持输入、 输出和输入/输出参数。 输出参数值在运行时（仅当没有行集返回时）或当应用程序用尽返回的所有行集时，返回到应用程序。 若要确保返回的值是有效的使用**IMultipleResults**强制行集消耗。  
  
 在 DBPARAMBINDINFO 结构中无需指定存储过程参数的名称。 使用 NULL 值的*pwszName*成员，表示 SQL Server 的 OLE DB 驱动程序应忽略的参数名称，并使用仅在指定的序号*rgParamOrdinals* 的成员**ICommandWithParameters::SetParameterInfo**。 如果命令文本中既包含命名参数又包含未命名参数，则必须在所有命名参数之前指定所有未命名参数。  
  
 如果指定的存储的过程参数的名称，则 SQL Server 的 OLE DB 驱动程序将检查以确保它是有效的名称。 在使用者接收错误参数名称时，SQL Server 的 OLE DB 驱动程序将返回错误。  
  
> [!NOTE]  
>  若要公开支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)，SQL Server 的 OLE DB 驱动程序实现一个新[ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
