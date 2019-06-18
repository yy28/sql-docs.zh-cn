---
title: Foreach 循环容器 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.f1
helpviewer_keywords:
- repeating control flow
- Foreach Loop containers
- foreach enumerators [Integration Services]
- containers [Integration Services], Foreach Loop
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bb50b4000397ca3dd51be58867e45135d1d587f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831570"
---
# <a name="foreach-loop-container"></a>Foreach 循环容器
  Foreach 循环容器定义包中的重复控制流。 循环的实现与编程语言中的 **Foreach** 循环结构类似。 在包中，通过使用 Foreach 枚举器启用循环。  Foreach 循环容器将重复指定枚举器的每个成员的控制流。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供了下列枚举器类型：  
  
-   Foreach ADO 枚举器，用于枚举表中的行。 例如，可以获取 ADO 记录集中的行。  
  
     数据集目标将数据保存在內存中的一个记录集中，该记录集存储在数据类型为 `Object` 的包变量中。 您通常使用具有 Foreach ADO 枚举器的 Foreach 循环容器来每次处理记录集的一行。 为 Foreach ADO 枚举器指定的变量必须为 Object 数据类型。 有关记录集目标的详细信息，请参阅 [Use a Recordset Destination](../data-flow/recordset-destination.md)。  
  
-   Foreach ADO.NET 架构行集枚举器，用于枚举有关数据源的架构信息。 例如，可枚举并获取一组 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中的表。  
  
-   Foreach 文件枚举器，用于枚举文件夹中的文件。 该枚举器可遍历子文件夹。 例如，可读取 Windows 文件夹及其子文件夹中所有具有 *.log 文件扩展名的文件。  
  
-   Foreach 源变量枚举器，用于枚举指定变量包含的可枚举对象。 可枚举对象可以是数组、ADO.NET `DataTable` 和 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 枚举器等。 例如，可以枚举包含服务器名称的数组中的值。  
  
-   Foreach 项枚举器，用于枚举集合项。 例如，可以枚举执行进程任务所使用的可执行文件和工作目录的名称。  
  
-   Foreach Nodelist 枚举器，用于枚举 XML Path 语言 (XPath) 表达式的结果集。 例如，此表达式可枚举并获取古代的所有作者： `/authors/author[@period='classical']`。  
  
-   Foreach SMO 枚举器，用于枚举 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 对象。 例如，可枚举并获取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中的视图列表。  
  
-   Foreach Azure Blob 枚举器，用于在 Azure 存储中的 blob 容器中枚举 blob。  
  
-   若要枚举的 ADLS 目录中的文件的 Foreach ADLS 文件枚举器。
  
 以下关系图显示了一个具有文件系统任务的 Foreach 循环容器。 该 Foreach 循环使用了 Foreach 文件枚举器，并将文件系统任务配置为复制文件。 如果枚举器指定的文件夹包含四个文件，则循环将重复四次，复制四个文件。  
  
 ![用于枚举文件夹的 Foreach 循环容器](../media/ssis-foreachloop.gif "A Foreach Loop container that enumerates a folder")  
  
 可以使用变量和属性表达式的组合，用枚举器集合值更新包对象的属性。 首先，将集合值映射到用户定义变量；然后，对使用该变量的属性执行一个属性表达式。 例如，Foreach 文件枚举器集合值映射到一个名为变量`MyFile`变量然后发送邮件任务的 Subject 属性使用属性表达式中。 如果运行该包，则每次重复循环时，都会用一个文件名更新 Subject 属性。 有关详细信息，请参阅 [在包中使用属性表达式](../expressions/use-property-expressions-in-packages.md)。  
  
 映射到枚举器集合值的变量也可用于表达式和脚本。  
  
 Foreach 循环容器可以包含多个任务和容器，但只能使用一种类型的枚举器。 如果 Foreach 循环容器包含多个任务，则可将枚举器集合值映射到每个任务的多个属性。  
  
 可以设置 Foreach 循环容器的事务属性，从而为包控制流的子集定义事务。 通过这种方式，可以在 Foreach 循环级别而不是包级别管理事务。 例如，如果 Foreach 循环容器重复了星形架构中的维度表和事实数据表的更新控制流，则可以配置事务以确保成功更新所有事实数据表，或者不更新任何事实数据表。 有关详细信息，请参阅 [Integration Services 事务](../integration-services-transactions.md)。  
  
## <a name="enumerator-types"></a>枚举器类型  
 枚举器可以配置，您必须为不同的枚举器提供不同的信息。  
  
 下表汇总了每种枚举器类型需要的信息。  
  
|枚举器|配置要求|  
|----------------|--------------------------------|  
|Foreach ADO|指定 ADO 对象源变量和枚举器模式。 该变量必须是 Object 数据类型。|  
|Foreach ADO.NET 架构行集|指定与数据库的连接和要枚举的架构。|  
|Foreach 文件|指定要枚举的文件夹和文件、检索到的文件的文件名格式，以及是否要遍历子文件夹。|  
|Foreach 源变量|指定包含要枚举的对象的变量。|  
|Foreach 项|定义 Foreach 项集合中的项，包括列和列数据类型。|  
|Foreach Nodelist|指定 XML 文档的源并配置 XPath 操作。|  
|Foreach SMO|指定与数据库的连接以及要枚举的 SMO 对象。|  
|Foreach Azure Blob|指定包含要枚举的 blob 的 Azure blob 容器。|  
|Foreach ADLS 文件|指定包含要枚举，以及一些筛选器文件的 ADLS 目录。|
  
## <a name="property-expressions-in-foreach-loop-containers"></a>Foreach 循环容器中的属性表达式  
 可以将包配置为并发运行多个可执行文件。 如果包中包含实现属性表达式的 Foreach 循环容器，则应当小心使用此配置。  
  
 通常需要实现属性表达式以便设置 Foreach 循环枚举器所使用的连接管理器的 ConnectionString 属性的值。 ConnectionString 的属性表达式是由映射到枚举器的集合值的变量来设置的，并在每个循环迭代中被更新。  
  
 若要避免在循环中并行执行任务时遇到不可确定的定时导致的负数结果，应当将包配置为每次只运行一个可执行文件。 例如，如果包可以并发运行多个任务，那么当一个 Foreach 循环容器枚举文件夹中的文件，然后检索文件名，然后使用执行 SQL 任务将文件名插入表中时，如果在两个执行 SQL 任务实例都试图同时写入，就有可能导致写入冲突。 有关详细信息，请参阅 [在包中使用属性表达式](../expressions/use-property-expressions-in-packages.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击以下主题之一：  
  
-   [配置 Foreach 循环容器](foreach-loop-container.md)  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
## <a name="related-content"></a>相关内容  
 bidn.com 上的博客文章 [用于各节点列表枚举器的 SSIS](https://go.microsoft.com/fwlink/?LinkId=220671)。  
  
## <a name="see-also"></a>请参阅  
 [控制流](control-flow.md)   
 [Integration Services 容器](integration-services-containers.md)  
  
  
