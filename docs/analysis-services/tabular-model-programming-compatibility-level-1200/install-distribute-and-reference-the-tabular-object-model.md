---
title: 安装、 分发和引用表格对象模型 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81f3b12aeb7cb6a185c0ee9b1152d75f3451c4b0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="install-distribute-and-reference-the-tabular-object-model"></a>安装、 分发和引用表格对象模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
此文章介绍了如何下载、 引用和重新分发 Analysis Services 表格对象模型 (TOM)，用于创建和管理表格模型和托管代码中的数据库的 C# 库。  
  
TOM 是附带 SQL Server 2016 的 AMO 客户端库 (Microsoft.AnalysisServices.dll) 的扩展。 它适用于表格模型以在 SQL Server 2016 版本表格元数据引擎为目标。 若要使用 TOM，模型和数据库必须处于兼容性级别为 1200年或更高版本。  

## <a name="amo-tom-assemblies"></a>AMO TOM 程序集

SQL Server 2016 重构，且会展开以包括新的核心、 表格和 JSON 程序集的 AMO。 它还包括原始 AMO 程序集，Microsoft.AnalysisServices.dll，其第一个版本以来已 Analysis Services 的一部分。 已重新组织的 AMO 可卸载到一个程序集的公共类，并提供逻辑划分表格和多维 Api 之间通过其他程序集。 

下表介绍每个程序集。
  
Assembly  |功能  |重要的类 |
---------|---------|--------------  |
核心 <br/>Microsoft.AnalysisServices.Core.dll | 表格和多维数据库所共有。 <br/><br/>提供的异常处理，泛型连接到 Analysis Services 实例和数据库，并且有权公共属性和方法的服务器和数据库对象。 <br/><br/>它具有所需的任何 AMO 解决方案针对 SQL Server 2016。 | 核心&nbsp;服务器<br/>核心&nbsp;数据库<br/>AmoException
TOM<br/> Microsoft.AnalysisServices.Tabular.dll、 版本 13.0.1601.5 或更高版本。| 创建和管理表格元数据对象。 | TOM&nbsp;服务器 <br/>TOM&nbsp;数据库<br /> Model<br /> 表<br /> 列<br /> 关系
  AMO<br /> Microsoft.AnalysisServices.dll| 创建和管理多维元数据对象，包括表格 1050年 1103年数据库。 | AMO&nbsp;服务器 <br />AMO&nbsp;数据库 <br /> 多维数据集 <br /> 维度 <br /> 度量值组 
Json<br/>Microsoft.AnalysisServices.Tabular.Json.dll | 帮助器的包装 NewtonSoftJson.dll (JSON.NET) 来控制更新，删除引入到 Analysis Services 工作负荷中的 JSON 序列化的功能更改的风险的 DLL。 <br /> <br />此 DLL 作为 TOM 中的依赖项存在，而且不应在代码中直接使用。 | 无。  
  
 ### <a name="understanding-assembly-dependencies"></a>了解程序集依赖项
  
若要对 AMO 编程，你的解决方案必须包括对依赖 Dll 的引用。 AMO 和 TOM 依赖于核心，因为它提供基类。

AMO 取决于 TOM 因为 AMO 中的某些类从 TOM 引用类。 例如，AMO 数据库对象都有属性的类型模型，TOM dll 中实现模型。 

![AMO TOM 依赖关系](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/amo-tom-dependencies.png)

不能将分配 Microsoft.AnalysisServices.dll 而无需 Microsoft.AnalysisServices.Tabular.dll，但你可以引用它们各自的命名空间，而其他。

### <a name="choosing-which-namespace-to-use-in-code"></a>选择的命名空间在代码中使用

在[对象层次结构](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)，任何数据库下的对象是通过模型对象，表格元数据构造或通过多维数据集、 维度或度量值组对象的某个多维元数据构造。 对于在服务器、 数据库、 角色或跟踪级别的高级操作，的选择要引用的命名空间将取决于工作负荷你的代码需要支持。

* 如果你的解决方案是兼容性级别为 1200年或更高版本，并且你使用的数据库对象必须提供对模型、 表、 列和表示为表格元数据构造的其他对象的访问，请使用 Tabular.Server 或表格。
* 如果这样的下游代码引用例如多维数据集、 数据源、 DataSourceViews 和维度的多维对象，请使用 AnalysisServices.Server 或 AnalysisServices.Database。

你将需要工具和应用程序支持的数据库和模型类型组合两个命名的空间。 

引用在代码中的核心命名空间是不必要的;核心中的类是基类，这些类以提供通用属性，如名称和说明，主要对象的创建。  
  
## <a name="determine-whether-amo-and-tom-installation-is-required"></a>确定是否需要进行 AMO 和 TOM 安装  
   
 AMO 和 TOM 被捆绑在一起的单个客户端库中。 如果你已安装的 SQL Server 2016 Analysis Services 实例、 客户端库中或面向 SQL Server 2016年实例的 SQL Server Data Tools 的版本，Microsoft.AnalysisServices.dll 已安装。  
  
 若要确定是否已安装的程序集，请检查以下任意位置：
* C:\Windows\Microsoft.NET\assembly\GAC_MSIL
* C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies
* C:\Program Files\Microsoft SQL Server\130\DTS\Tasks
* C:\Program Files\Microsoft SQL Server\MSAS13。MSSQLSERVER\OLAP\bin
 
 验证存在以下程序集：
*  Microsoft.AnalysisServices.Core.dll
*  Microsoft.AnalysisServices.dll
*  Microsoft.AnalysisServices.Tabular.dll
*  Microsoft.AnalysisServices.Tabular.Json.dll   
   
## <a name="download-sqlasamo"></a>下载 SQL_AS_AMO  
 
 请注意，Microsoft.AnalysisServices.dll 不是可通过 NuGet 管理器。
  
1. 转到[的 SQL Server 2016 功能包下载页](https://www.microsoft.com/download/details.aspx?id=52676)。  
  
2. 单击 **“下载”**。  
  
3. 选择 **\X64\SQL_AS_AMO.msi**或 **\X86\SQL_AS_AMO.msi**。 你可以选择其中之一： AMO 和 TOM 程序集是以非特定于平台的。
  
4. 单击**下一步**继续进行下载。 你将发现中的.msi 文件你**下载**文件夹。  
  
## <a name="install-sqlasamo"></a>安装 SQL_AS_AMO  
  
1. 双击**SQL_AS_AMO.msi**并单步执行安装。  
  
2. 转到**C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies**以确认 Microsoft.AnalysisServices.Core.dll、 Microsoft.AnalysisServices.dll、 Microsoft.AnalysisServices.Tabular.dll，放置和Microsoft.AnalysisServices.Tabular.Json.dll。   
  
## <a name="add-references"></a>添加引用  
  
1. 在**解决方案资源管理器** > **添加引用** > **浏览**。  
2. 转到**C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** ，然后选择：  
   * Microsoft.AnalysisServices.Core  
   * Microsoft.AnalysisServices.Tabular  
   * Microsoft.AnalysisSerivces.Tabular.Json  
  
3. 单击 **“确定”**。  在**解决方案资源管理器**，确认在引用文件夹中存在的程序集。
  
4. 在代码页中，添加 Microsoft.AnalysisServces.Tabular 命名空间，如果数据库和模型是表格 1200年或更高的兼容性级别。 
  
   ```   
   using Microsoft.AnalysisServices; 
   using Microsoft.AnalysisServices.Tabular;
   ```  
    或者，添加 Microsoft.AnalysisServces 来支持更广泛的一组连接到不是专门在表格服务器模式下的 SQL Server 2016 的 Analysis Services 的实例。 
 
    当包括服务器、 数据库、 角色和跟踪的对象的类具有共同的命名空间，避免不明确的引用通过限定你想要使用的命名空间 （例如，Microsoft.AnalysisServices.Tabular.Server 实例化服务器对象使用的表格命名空间的）。

## <a name="redistribute-amo-and-tom-with-your-application"></a>利用你的应用程序重新发布 AMO 和 TOM  
  
重新分发的 AMO 和 TOM 是通过**sql_as_amo.msi**安装包。 如果要到 AMO 或 TOM 生成客户端调用的应用程序的安装程序，将添加**sql_as_amo.msi**到可执行文件。 这是用于重新分发的 AMO 和 TOM 客户端库的唯一受支持的机制。  
  
包是独立的并提供所需的代码中调用 AMO 和 TOM 的所有程序集。 其他包，例如 SQL_AS_OLEDB.msi 或 SQL_AS_ADOMD.msi，不是专门 TOM 编程方案所必需的。
