---
title: 公共语言运行时（CLR）集成的使用方案和示例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- scenarios [CLR integration]
- common language runtime [SQL Server], samples
- examples [CLR integration]
- sample applications [CLR integration]
- database objects [CLR integration], samples
- managed code [SQL Server], samples
ms.assetid: 33aac25f-abb4-4f29-af88-4a0dacd80ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3718a084211e7c3b2b7a14973e195a4b1c3b6b1a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62780707"
---
# <a name="usage-scenarios-and-examples-for-common-language-runtime-clr-integration"></a>公共语言运行时 (CLR) 集成的使用方案和示例
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括可以用来了解公共语言运行时 (CLR) 集成的可编程性功能的示例应用程序、包示例和多个编码示例。  
  
 有关实现这些示例和其他材料的完整 Visual Studio 项目，请访问[CodePlex 上 Microsoft SQL Server 社区项目 & 示例](https://go.microsoft.com/fwlink/?LinkID=193935)。  
  
|名称|说明|  
|----------|-----------------|  
|[从 CLR UDF 访问本机代码](../../../2014/database-engine/dev-guide/accessing-native-code-from-a-clr-udf.md)|显示如何从用户定义函数（该函数位于您的数据库的程序集中）调用本机（非托管） C++ 代码中的函数。|  
|[数组参数示例](../../../2014/database-engine/dev-guide/array-parameter-sample.md)|说明如何通过将客户端上的一组信息传递到服务器上的 CLR 集成存储过程来创建、更新或删除数据库中的行集。 这是通过使用 UDT 完成的。|  
|[日历感知日期和时间 UDT 示例](../../../2014/database-engine/dev-guide/calendar-aware-date-and-time-udt-sample.md)|定义了两种 UDT，通过它们可以按日历方式对日期和时间进行处理。|  
|[CLR 事务示例](../../../2014/database-engine/dev-guide/clr-transactions-sample.md)|说明了如何使用 System.Transactions 命名空间中的托管 API 来控制事务。|  
|[使用 CLR 和 XML 创建联系信息](../../../2014/database-engine/dev-guide/contact-creation-using-clr-and-xml.md)|SQL Server 的联系人示例提供了一些有用的实用工具，这些实用工具在基本的 AdventureWorks2012 示例数据库之上形成了一层额外的功能。 第一个实用工具为 AdventureWorks2012 数据库中所涉及的各种类型的人创建联系记录。 联系信息通过使用 XML 来指定，并传递到基于 C# 的存储过程或 VB 存储过程，以创建 XML 并将其放入该数据库中的正确表。|  
|[Currency 类型和转换函数](../../../2014/database-engine/dev-guide/currency-type-and-conversion-function.md)|使用 C# 定义 Currency 用户定义数据类型。|  
|[使用 CLR 处理大型对象](../../../2014/database-engine/dev-guide/handling-large-objects-using-clr.md)|演示如何使用 CLR 存储过程在与服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可访问的文件系统之间传输大型二进制对象（lob）。|  
|[Hello World Ready 示例](../../../2014/database-engine/dev-guide/hello-world-ready-sample.md)|说明创建、部署和测试基于 CLR 集成的简单且全球通用存储过程的基本操作。|  
|[Hello World 示例](../../../2014/database-engine/dev-guide/hello-world-sample.md)|说明创建、部署和测试基于 CLR 集成的简单存储过程的基本操作。|  
|[进程内数据访问示例](../../../2014/database-engine/dev-guide/in-process-data-access-sample.md)|包含多个演示 CLR 进程内数据访问接口的各种功能的简单函数。|  
|[结果集示例](../../../2014/database-engine/dev-guide/result-set-sample.md)|说明如何在通读查询结果时执行命令，而不需要打开新的连接并将所有结果读入内存。|  
|[发送数据集示例](../../../2014/database-engine/dev-guide/send-dataset-sample.md)|说明如何在服务器端基于 CLR 的存储过程中将基于 ADO.NET 的数据集作为结果集返回到客户端。|  
|[字符串实用工具函数示例](../../../2014/database-engine/dev-guide/string-utility-functions-sample.md)|包含一个流式表值函数 (TVF)，它是用 Visual C# 和 Visual Basic 编写的，可以将逗号分隔的字符串拆分到只有一列的表中。|  
|[能够识别增补字符的字符串操作示例](../../../2014/database-engine/dev-guide/supplementary-aware-string-manipulation-sample.md)|说明如何实现可以处理 Unicode 字符串和代理字符串的五个识别增补字符的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 字符串函数。|  
|[UDT 实用工具](../../../2014/database-engine/dev-guide/udt-utilities.md)|包含多个用户定义数据类型 (UDT) 的实用工具函数。|  
|[清除未使用的程序集](../../../2014/database-engine/dev-guide/unused-assembly-cleanup.md)|包含 .NET 存储过程，此存储过程用来通过查询元数据目录来删除当前数据库中未使用的程序集。|  
|[用户定义类型](../../../2014/database-engine/dev-guide/user-defined-type.md)|说明如何在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和使用 System.Data.SqlClient 的客户端应用程序中创建和使用简单 UDT。|  
|[UTF8 字符串用户定义数据类型 &#40;UDT&#41;](../../../2014/database-engine/dev-guide/utf8-string-user-defined-data-type-udt.md)|说明如何实现用于扩展数据库的类型系统以便存储 UTF8 编码的值的 UDT。|  
  
  
