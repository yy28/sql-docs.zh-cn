---
title: CLR 用户定义类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- validation [CLR integration]
- types [CLR integration]
- UserDefined serialization format [CLR integration]
- null values [CLR integration]
- serialization
- Native serialization format [CLR integration]
- databases [CLR integration]
- building database objects [CLR integration], user-defined types
- user-defined types [CLR integration]
- common language runtime [SQL Server], user-defined types
- UDTs [CLR integration]
- database objects [CLR integration], user-defined types
- turning on CLR functionality
- customizing UDT expression return types [CLR integration]
- UDTs [CLR integration], about UDTs
- comparing UDT values
- annotations [CLR integration]
- user-defined types [CLR integration], about UDTs
- variables [CLR integration]
- invoking UDT methods
- indexes [CLR integration]
ms.assetid: 27c4889b-c543-47a8-a630-ad06804f92df
author: rothja
ms.author: jroth
ms.openlocfilehash: 2078b11b44232b44e94191c07fca91998f2c1172
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028348"
---
# <a name="clr-user-defined-types"></a>CLR 用户定义类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使您能够创建针对在 .NET Framework 公共语言运行时（CLR）中创建的程序集进行编程的数据库对象。 数据库对象包括触发器、存储过程、函数、聚合函数和类型，它们可以利用 CLR 提供的丰富的编程模型。  
  
> [!NOTE]  
>  默认情况下，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中关闭了执行 CLR 代码的功能。 可以使用**sp_configure**系统存储过程来启用 CLR。  
  
 从开始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，你可以使用用户定义的类型（udt）来扩展服务器的标量类型系统，从而能够在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中存储 CLR 对象。 UDT 可以包含多个元素，还可以有行为，这使它们与由单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型组成的传统别名数据类型区分开来。  
  
 因为 UDT 作为整体供系统访问，所以其对复杂数据类型的使用可能会对性能有负面影响。 通常，使用传统的行和表可以对复杂数据进行最佳建模。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 UDT 非常适合以下各项：  
  
-   日期、时间、货币和扩展数字类型  
  
-   地理空间应用程序  
  
-   编码或加密数据  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中开发 UDT 的过程由以下步骤组成：  
  
1.  **编码和生成定义 UDT 的程序集。** 使用生成可验证代码的 .NET Framework 公共语言运行时 (CLR) 所支持的任何语言都可以定义 UDT， 这包括 Visual C# 和 Visual Basic .NET。 数据作为 .NET Framework 类或结构的字段和属性公开，其行为由类或结构的方法定义。  
  
2.  **注册程序集。** 可以通过在数据库项目中使用 Visual Studio 用户界面，或通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 语句（该语句将包含类或结构的程序集复制到数据库中），来部署 UDT。  
  
3.  **在 SQL Server 中创建 UDT。** 一旦程序集加载到宿主数据库中，则使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE 语句创建 UDT，并将该类或结构的成员作为此 UDT 的成员公开。 UDT 仅在单个数据库的上下文中存在，一旦注册，则不依赖于从其创建它们的外部文件。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前，不支持从 .NET Framework 程序集创建的 UDT。 不过，你仍然可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sp_addtype**来使用别名数据类型。 本机 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户定义数据类型和 UDT 都可以用 CREATE TYPE 语法创建。  
  
4.  **使用 UDT 创建表、变量或参数**从开始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，用户定义类型可用作表的列定义、 [!INCLUDE[tsql](../../includes/tsql-md.md)]批处理中的变量，或者用作[!INCLUDE[tsql](../../includes/tsql-md.md)]函数或存储过程的参数。  
  
## <a name="in-this-section"></a>本节内容  
 [Creating a User-Defined Type（创建用户定义类型）](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
 描述如何创建 UDT。  
  
 [在 SQL Server 中注册用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/registering-user-defined-types-in-sql-server.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册和管理 UDT。  
  
 [使用 SQL Server 中的用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
 描述如何使用 UDT 创建查询。  
  
 [在 ADO.NET 中访问用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-in-ado-net.md)  
 描述如何在 ADO.NET 中使用用于 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来处理 UDT。  
  
  
