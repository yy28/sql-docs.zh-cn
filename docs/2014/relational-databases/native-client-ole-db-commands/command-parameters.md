---
title: 命令参数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- parameters [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, parameters
- SQL Server Native Client OLE DB provider, commands
- parameters [SQL Server Native Client], OLE DB
- commands [OLE DB]
ms.assetid: 072ead49-ebaf-41eb-9a0f-613e9d990f26
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2ae43260105acca3d638749d197e4e0d95a0260
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426826"
---
# <a name="command-parameters"></a>命令参数
  在命令文本中参数用问号字符标记。 例如，以下 SQL 语句标记了单个输入参数：  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 通过减少网络流量来提高性能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序不会自动派生参数信息除非**icommandwithparameters:: Getparameterinfo**或**Icommandprepare:: Prepare**执行命令之前调用。 这意味着， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不会自动：  
  
-   验证与指定的数据类型的正确性**icommandwithparameters:: Setparameterinfo**。  
  
-   将取值函数绑定信息中指定的 DBTYPE 映射到参数的正确 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。  
  
 如果这两个方法指定的数据类型与参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不兼容，那么应用程序在使用该方法时将可能收到错误或产生精度损失。  
  
 若要确保不发生这种情况，应用程序应当：  
  
-   絋粄*pwszDataSourceType*匹配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型的参数，如果硬编码**icommandwithparameters:: Setparameterinfo**。  
  
-   如果硬编码取值函数，则应确保绑定到参数的 DBTYPE 值与参数的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型具有相同类型。  
  
-   要调用的应用程序的代码**icommandwithparameters:: Getparameterinfo** ，以便该提供程序可以获取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型的参数的动态。 请注意，这会导致与服务器之间额外的网络往返。  
  
> [!NOTE]  
>  提供程序不支持调用**icommandwithparameters:: Getparameterinfo**任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UPDATE 或 DELETE 语句包含 FROM 子句; 用于任何 SQL 语句，具体取决于包含参数; 的子查询对于 SQL 语句中包含参数标记的比较，这两个表达式类似，或包含限定谓词;或其中一个参数是一个函数的参数的查询。 在处理一批 SQL 语句时，该提供程序也不支持调用**icommandwithparameters:: Getparameterinfo**批处理中的第一个语句后的语句中的参数标记。 注释 (/ * \*/) 中不允许使用[!INCLUDE[tsql](../../includes/tsql-md.md)]命令。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持 SQL 语句命令中的输入的参数。 过程调用命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口支持输入、 输出和输入/输出参数。 输出参数值在运行时（仅当没有行集返回时）或当应用程序用尽返回的所有行集时，返回到应用程序。 若要确保返回的值有效，请使用**IMultipleResults**来强制使用行集。  
  
 在 DBPARAMBINDINFO 结构中无需指定存储过程参数的名称。 使用的值为 NULL *pwszName*成员，指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序应忽略参数名和使用仅在指定的序号*rgParamOrdinals*的成员**icommandwithparameters:: Setparameterinfo**。 如果命令文本中既包含命名参数又包含未命名参数，则必须在所有命名参数之前指定所有未命名参数。  
  
 如果指定的存储的过程参数名称，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口会检查以确保其有效的名称。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从使用者接收错误的参数名称时，Native Client OLE DB 提供程序返回错误。  
  
> [!NOTE]  
>  若要公开的支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序实现了新[ISSCommandWithParameters](../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [命令](commands.md)  
  
  
