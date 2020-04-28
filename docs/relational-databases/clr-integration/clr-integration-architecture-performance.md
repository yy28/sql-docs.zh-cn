---
title: CLR 集成的性能 |Microsoft Docs
description: 本文介绍与 .NET Framework CLR 的 Microsoft SQL Server 集成的设计选择，包括编译过程和性能。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
author: rothja
ms.author: jroth
ms.openlocfilehash: ac12bf75588d70f12b4550260f9911796c1c3a56
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488142"
---
# <a name="clr-integration-architecture----performance"></a>CLR 集成体系结构 - 性能
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  本主题讨论一些可提高与[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 公共语言运行时（CLR）集成性能的设计选择。  
  
## <a name="the-compilation-process"></a>编译过程  
 在编译 SQL 表达式时，如果遇到对托管例程的引用，则生成 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 中间语言 (MSIL) 存根。 该存根包含的代码用于将例程参数从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 封送到 CLR、调用函数并返回结果。 该“粘附”代码基于参数类型和参数方向（向内、向外或引用）。  
  
 粘附代码支持特定于类型的优化，并确保有效地强制实现 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语义，例如为 Null 性、约束方面、按值和标准异常处理。 通过为确切类型的参数生成代码，可以避免跨调用边界的类型强制或包装对象创建开销（称为“装箱”）。  
  
 随后，使用 CLR 的 JIT（实时）编译服务将生成的存根编译为本机代码，并针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行所在的特定硬件体系结构进行优化。 JIT 服务是在方法级别调用的，并允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 宿主环境创建一个跨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 执行的编译单元。 编译存根之后，生成的函数指针即成为函数的运行时实现。 此代码生成方法确保不会发生与运行时反射或元数据访问相关的其他调用开销。  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>在 SQL Server 和 CLR 之间快速转换  
 编译过程生成的函数指针可以在运行时通过本机代码调用。 对于标量值用户定义函数，可基于每行调用此函数。 为最大程度地降低在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 之间转换的成本，包含任何托管调用的语句都具有一个标识目标应用程序域的启动步骤。 该标识步骤减少每行的转换成本。  
  
## <a name="performance-considerations"></a>性能注意事项  
 以下内容概述了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中特定于 CLR 集成的性能注意事项。 MSDN 网站上的 "[使用 CLR 集成 SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=50332)" 中可找到更详细的信息。 有关托管代码性能的常规信息，请参阅 MSDN 网站上的 "[改进 .Net 应用程序的性能和可伸缩性](https://go.microsoft.com/fwlink/?LinkId=50333)"。  
  
### <a name="user-defined-functions"></a>用户定义函数  
 相较于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 用户定义函数，CLR 函数可以从更快的调用路径中受益。 此外，同 [!INCLUDE[tsql](../../includes/tsql-md.md)] 相比，托管代码在过程代码、计算和字符串操作方面具有决定性性能优势。 需要大量计算且不执行数据访问的 CLR 函数采用托管代码编写的效果更好。 但是与 CLR 集成相比，[!INCLUDE[tsql](../../includes/tsql-md.md)] 函数的确可以更有效地执行数据访问。  
  
### <a name="user-defined-aggregates"></a>用户定义聚合  
 托管代码的性能大大优于基于游标的聚合。 托管代码的执行速度通常稍慢于内置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 聚合函数的执行速度。 如果存在本机内置聚合函数，建议您使用该函数。 对于所需聚合不受本机支持的情况，出于性能原因，请考虑使用 CLR 用户定义聚合，而不是基于游标的实现。  
  
### <a name="streaming-table-valued-functions"></a>流式表值函数  
 应用程序通常需要返回一个表作为调用函数的结果。 示例包括从文件读取表格格式数据作为导入操作的一部分，并将逗号分隔值转换为关系表示形式。 通常，您可以通过在调用方使用结果表之前具体化和填充此结果表来实现此目的。 CLR 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的集成引入了一种名为流式表值函数 (STVF) 的新扩展性机制。 托管 STVF 的性能优于可比扩展存储过程实现的性能。  
  
 Stvf 是返回**IEnumerable**接口的托管函数。 **IEnumerable**包含用于导航 STVF 返回的结果集的方法。 调用 STVF 时，返回的**IEnumerable**直接连接到查询计划。 查询计划在需要提取行时调用**IEnumerable**方法。 使用此迭代模型，结果在第一行生成之后即可使用，而不需要等到整个表填充完。 还可以极大地减少调用该函数而占用的内存。  
  
### <a name="arrays-vs-cursors"></a>数组与游标  
 当 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标必须遍历更容易表示为数组的数据时，使用托管代码可以显著提高性能。  
  
### <a name="string-data"></a>字符串数据  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符数据（如**varchar**）的类型可以是 SqlString 或 SqlChars。 SqlString 变量将整个值的实例创建到内存中。 SqlChars 变量提供可用于获得更好性能和可扩展性的流式接口，而无需将整个值的实例创建到内存中。 这对于大型对象 (LOB) 数据尤为重要。 此外，可以通过**CreateReader （）** 返回的流接口访问服务器 XML 数据。  
  
### <a name="clr-vs-extended-stored-procedures"></a>CLR 与扩展存储过程  
 允许托管过程向客户端回发结果集的 Microsoft.SqlServer.Server 应用程序编程接口 (API) 的性能优于扩展存储过程使用的开放式数据服务 (ODS) API。 此外，System.web Api 还支持[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中引入的**xml**、 **varchar （max）**、 **nvarchar （max）** 和**VARBINARY （max**）等数据类型，而 ODS api 尚未进行扩展以支持新的数据类型。  
  
 通过托管代码，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对内存、线程和同步等资源的使用。 这是因为公开这些资源的托管 API 是针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源管理器实现的。 相反，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法查看或控制扩展存储过程的资源使用情况。 例如，如果扩展存储过程占用过多 CPU 或内存资源，则无法通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 检测或控制此种情况。 但是，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用托管代码检测到给定线程已有很长一段时间未生成结果，并强制该任务生成以便安排其他工作。 因此，使用托管代码可以提高可扩展性，并改善系统资源使用情况。  
  
 托管代码可能带来维护执行环境和执行安全检查所需的额外开销。 例如，当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内运行并需要执行从托管代码到本机代码的大量转换时，可能会发生此种情况（因为在托管代码和本机代码之间来回转换时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要对特定于线程的设置进行额外维护）。 因此，对于在托管代码和本机代码之间进行频繁转换的情况，扩展存储过程的性能大大优于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内运行的托管代码的性能。  
  
> [!NOTE]  
>  建议您不要开发新的扩展存储过程，因为已不推荐使用此功能。  
  
### <a name="native-serialization-for-user-defined-types"></a>用户定义类型的本机序列化  
 用户定义类型 (UDT) 是作为标量类型系统的扩展性机制设计的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实现称为**format**的 udt 的序列化格式。 在编译期间，检查该类型的结构以便生成针对该特定类型定义自定义的 MSIL。  
  
 本机序列化是针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实现。 用户定义序列化调用由类型作者定义的方法来执行序列化。 **格式。** 应尽可能使用本机序列化，以获得最佳性能。  
  
### <a name="normalization-of-comparable-udts"></a>可比 UDT 的规范化  
 关系操作（例如对 UDT 进行排序和比较）是针对值的二进制表示形式直接执行的。 通过在磁盘上存储 UDT 状态的规范化（二进制排序）表示形式可以实现此目的。  
  
 规范化具有两个优点：避免构造类型实例和方法调用开销，进而极大地降低了比较操作的成本；为 UDT 创建二进制域，支持构造直方图、索引以及该类型的值的直方图。 因此，规范化 UDT 的性能配置文件类似于未涉及方法调用的操作的本机内置类型性能配置文件。  
  
### <a name="scalable-memory-usage"></a>可扩展内存使用量  
 为了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中很好地执行和调整托管垃圾回收，请避免使用大型单一分配。 大小大于 88 千字节 (KB) 的分配将被放置到大对象堆，这将导致垃圾回收的性能和调整结果远不如多个较小分配的性能和调整结果。 例如，如果需要分配一个大型多维数组，最好分配一个交错（分散）数组。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
