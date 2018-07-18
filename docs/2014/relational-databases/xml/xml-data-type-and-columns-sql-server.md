---
title: XML 数据类型和列 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 00db8f21-7d4b-4347-ae43-3a7c314d2fa1
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fe03ba5bafde60d2a653e49bcfe90b70978a25d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300027"
---
# <a name="xml-data-type-and-columns-sql-server"></a>XML 数据类型和列 (SQL Server)
  本主题讨论的优势和限制`xml`中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并帮助您选择如何存储 XML 数据。  
  
## <a name="relational-or-xml-data-model"></a>关系或 XML 数据模型  
 如果您的数据已通过已知架构高度结构化，则关系模型可能最适合用于数据存储。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了您所需的必要功能和工具。 另一方面，如果结构是半结构化或非结构化的或者未知的，则必须考虑对这类数据进行建模。  
  
 如果您需要一个与平台无关的模型，以便通过使用结构和语义标记来确保数据的可移植性，则 XML 是一个不错的选择。 此外，下列情况下，适于做此选择：  
  
-   您的数据为稀疏数据，或您不了解数据的结构，或数据结构将来可能会有重大变化。  
  
-   您的数据体现的是包容层次结构而不是在实体间的引用，并且可能是递归数据。  
  
-   您的数据本身具有顺序性。  
  
-   您希望基于数据的结构查询数据或更新部分数据。  
  
 如果上述条件均不满足，则应使用关系数据模型。 例如，如果你的数据采用 XML 格式，但你的应用程序只使用数据库来存储和检索数据，`[n]varchar(max)`列为所有需要。 将数据存储在 XML 列中还有其他好处， 包括让引擎确定数据格式是否正确或有效，以及支持对 XML 数据进行精细查询和更新。  
  
## <a name="reasons-for-storing-xml-data-in-sql-server"></a>在 SQL Server 中存储 XML 数据的理由  
 下面是一些使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的本机 XML 功能而不是在文件系统中管理 XML 数据的理由：  
  
-   您希望以一种高效的事务处理方式来共享、查询和修改 XML 数据。 精细的数据访问对于您的应用程序而言很重要。 例如，您可能需要提取 XML 文档中的某些部分，或者您可能需要插入新的部分而不是替换整个文档。  
  
-   您有关系数据和 XML 数据，希望在应用程序中进行关系数据和 XML 数据之间的互操作。  
  
-   您需要语言支持，以便对于跨域应用程序可以进行查询和数据修改。  
  
-   您希望服务器能够保证数据格式正确，并能够视情况根据 XML 架构来验证您的数据。  
  
-   您希望对 XML 数据创建索引以实现高效的查询处理和良好的可伸缩性，并使用一流查询优化器。  
  
-   您希望对 XML 数据进行 SOAP、ADO.NET 和 OLE DB 访问。  
  
-   您希望使用数据库服务器的管理功能来管理 XML 数据。 例如，这可能是备份、恢复和复制。  
  
 如果未满足这些条件中的任意一个，则最好是将数据存储为非 XML 数据，这是一种大型对象类型（如 `[n]varchar(max)` 或 `varbinary(max)`）。  
  
## <a name="xml-storage-options"></a>XML 存储选项  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XML 存储选项包括：  
  
-   本机存储，数据类型为 `xml`  
  
     数据以保留数据的 XML 内容的内部表示形式进行存储， 这种内部表示形式包括包容层次结构、文档顺序、元素和属性值的相关信息。 具体来说，就是保留 XML 数据的 InfoSet 内容。 有关信息集的详细信息，请访问 [http://www.w3.org/TR/xml-infoset](http://go.microsoft.com/fwlink/?LinkId=48843)。 InfoSet 内容并不是文本 XML 的精确副本，因为其中未保留下列信息：无关紧要的空格、属性顺序、命名空间前缀和 XML 声明。  
  
     对于类型化`xml`数据类型，`xml`数据类型绑定到 XML 架构后, 架构验证信息集 (PSVI) 将类型信息添加到信息集，并按内部表示形式进行编码。 这会显著提高分析速度。 有关详细信息，请参阅位于 [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?LinkId=48881) 和 [http://www.w3.org/TR/xmlschema-2](http://go.microsoft.com/fwlink/?LinkId=4871) 的 W3C XML 架构规范。  
  
-   在 XML 和关系存储之间映射  
  
     通过使用带批注的架构 (AXSD)，将 XML 分解到一个或多个表中的列。 这可保留在关系级别上的数据保真度。 因此，尽管忽略了元素间的顺序，但仍保留了层次结构。 架构不能是递归的。  
  
-   大型对象存储（`[n]varchar(max)` 和 `varbinary(max)`）  
  
     存储数据的精确副本。 这对于特殊用途的应用（如法律文档）很有用。 大多数应用不需要完全相同的副本，且 XML 内容（InfoSet 保真度）即可满足需要。  
  
 通常，您必须结合使用这些方法。 例如，你可能想要将 XML 数据存储在`xml`数据类型列，并将属性从其提升到关系列。 或者，可能想要使用映射技术将非递归部分存储中的非 XML 列，仅在将递归部分存储`xml`数据类型列。  
  
### <a name="choice-of-xml-technology"></a>XML 技术的选择  
 XML 技术（本机 XML 与 XML 视图）的选择通常取决于下列因素：  
  
-   存储选项  
  
     您的 XML 数据可能更适于大型对象存储（例如，产品手册），或更适于存储在关系列中（例如，转换为 XML 的行项）。 每个存储选项都在不同程度上保留文档保真度。  
  
-   查询功能  
  
     您可能会发现，基于查询的特性和对 XML 数据进行查询的程度，某一个存储选项比其他选项更合适。 在两个存储选项中，对 XML 数据的精细查询（例如，XML 节点上的谓词评估）得到不同程度的支持。  
  
-   对 XML 数据创建索引  
  
     您可能希望对 XML 数据创建索引以提高 XML 查询的性能。 索引选项随存储选项的不同而不同，您必须做出适当的选择才能优化工作负荷。  
  
-   数据修改功能  
  
     某些工作负荷涉及对 XML 数据进行精细修改。 例如，在文档中添加新的部分，而其他工作负荷（如 Web 内容）则不涉及。 对于您的应用程序来说，数据修改语言支持可能很重要。  
  
-   架构支持  
  
     您的 XML 数据可通过架构进行说明，该架构可能是 XML 架构文档，也可能不是。 对绑定到架构的 XML 的支持取决于 XML 技术。  
  
 此外，不同的选择具有不同的性能特征。  
  
### <a name="native-xml-storage"></a>本机 XML 存储  
 您可以将 XML 数据存储在`xml`在服务器上的数据类型列。 下列情况下，适于做此选择：  
  
-   您希望使用一种简单的方法将 XML 数据存储在服务器上，同时保留文档顺序和文档结构。  
  
-   您可能有对应于您的 XML 数据的架构，也可能没有。  
  
-   您希望查询和修改 XML 数据。  
  
-   您希望对 XML 数据创建索引，以提高查询处理的速度。  
  
-   您的应用程序需要系统目录视图以管理您的 XML 数据和 XML 架构。  
  
 如果您的 XML 文档具有多种结构，或您的 XML 文档符合不同的或复杂的架构，而这些架构很难映射到关系结构，本机 XML 存储很有用。  
  
#### <a name="example-modeling-xml-data-using-the-xml-data-type"></a>示例：使用 xml 数据类型对 XML 数据进行建模  
 例如有一个 XML 格式的产品手册，其中每个主题对应单独的一章，而每章中又包含多节。 一节可以包含多个小节。 因此，\<section> 是一个递归元素。 产品手册包含大量混合内容、关系图和技术材料；数据是半结构化的。 用户可能希望对感兴趣的主题执行上下文搜索，例如，在有关“索引”的章中搜索有关“聚集索引”的节，并查询技术数量。  
  
 适合 XML 文档的存储模型为 `xml` 数据类型列。 这可保留 XML 数据的 InfoSet 内容。 对 XML 列创建索引有利于提高查询性能。  
  
#### <a name="example-retaining-exact-copies-of-xml-data"></a>示例：保留 XML 数据的精确副本  
 为了进行说明，假定政府条例要求您保留 XML 文档的精确文本副本。 例如，这些文档可能为签署的文档、法律文档或股票交易单。 你可能想要将文档存储在`[n]varchar(max)`列。  
  
 对于查询，可以在运行时将数据转换为 `xml` 数据类型并针对此数据执行 Xquery。 运行时转换开销可能很高，尤其是在文档较大的情况下更是如此。 如果要频繁查询，则可以另外将文档存储在 `xml` 数据类型列中，并在从 `[n]varchar(max)` 列返回精确的文档副本时对文档创建索引。  
  
 XML 列可能是计算的列，基于`[n]varchar(max)`列。 但是，不能对计算得出的 XML 列创建 XML 索引，也可以生成 XML 索引`[n]varchar(max)`或`varbinary(max)`列。  
  
### <a name="xml-view-technology"></a>XML 视图技术  
 通过定义 XML 架构和数据库中的表之间的映射，可以创建持久性数据的“XML 视图”。 通过 XML 视图，可使用 XML 大容量加载来填充基础表。 您可以使用 XPath 1.0 版来查询 XML 视图；这种查询将被转换为针对表的 SQL 查询。 与此类似，更新也会被传播到那些表。  
  
 在下列情况下，此技术很有用：  
  
-   您需要拥有以 XML 为中心的编程模型，该模型使用建立在现有关系数据上的 XML 视图。  
  
-   您有对应于您的 XML 数据的架构（XSD、XDR），该架构可能由外部伙伴提供。  
  
-   数据中的顺序并不重要，或查询表数据不是递归的，或事先已知最大递归深度。  
  
-   您希望使用 XPath 1.0 版通过 XML 视图查询和修改数据。  
  
-   您希望通过 XML 视图来大容量加载 XML 数据，并将其分解到基础表。  
  
 这方面的例子有，作为用于数据交换和 Web 服务的 XML 公开的关系数据，以及具有固定架构的 XML 数据。 有关详细信息，请参阅 [MSDN Online Library](http://go.microsoft.com/fwlink/?linkid=31174)。  
  
#### <a name="example-modeling-data-using-an-annotated-xml-schema-axsd"></a>示例：使用带批注的 XML 架构 (AXSD) 对数据进行建模  
 为了进行说明，假定您具有希望将其作为 XML 处理的关系数据（如客户、订单和行项）。 请使用 AXSD 在关系数据上定义 XML 视图。 通过使用 XML 视图可以将 XML 数据大容量加载到表，以及使用 XML 视图查询和更新关系数据。 如果必须在 SQL 应用程序不间断工作时与其他应用程序交换包含 XML 标记的数据，该模型很有用。  
  
### <a name="hybrid-model"></a>混合模型  
 通常情况下，关系的组合和`xml`数据类型列是适用于数据建模。 可以将 XML 数据中的某些值存储在关系列中，而将其余或全部 XML 值存储在 XML 列中。 这可获得更好的性能，您可以更好地控制对关系列创建的索引和锁定特征。  
  
 要存储在关系列中的值取决于您的工作负荷。 例如，如果根据路径表达式 /Customer/@CustId 检索所有 XML 值，则将 **CustId** 属性的值提升到关系列并对其进行索引可以获得更快的查询性能。 另一方面，如果您的 XML 数据是以非冗余方式广泛地分解在关系列中，则重新汇集的开销可能很大。  
  
 对于高度结构化的 XML 数据，例如，表的内容已转换为 XML，您可以将所有值映射到关系列，并且可能使用 XML 视图技术。  
  
## <a name="granularity-of-xml-data"></a>XML 数据的粒度  
 XML 列中存储的 XML 数据的粒度对锁定至关重要，在一定程度上，对更新也很重要。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对 XML 数据和非 XML 数据都使用相同的锁定机制。 因此，行级锁定会导致锁定行中的所有 XML 实例。 当粒度较大时，锁定大型 XML 实例以便进行更新会导致多用户情况下的吞吐量下降。 另一方面，过度分解会丢失对象封装，并增加重新汇集开销。  
  
 对于良好的设计而言，重要的是保持数据建模要求与锁定和更新特征之间的平衡。 但在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，实际存储的 XML 实例的大小并不十分重要。  
  
 例如，通过使用对部分二进制大型对象 (BLOB) 和部分索引更新（将存储的现有 XML 实例与其更新后的版本进行比较）的新支持，对 XML 实例进行更新。 部分二进制大型对象 (BLOB) 更新在两个 XML 实例之间执行差异比较，并只更新差异之处。 部分索引更新只修改那些必须在 XML 索引中更改的行。  
  
## <a name="limitations-of-the-xml-data-type"></a>xml 数据类型的限制  
 请注意以下适用于 `xml` 数据类型的一般限制：  
  
-   存储的表示形式`xml`数据类型实例不能超过 2 GB。  
  
-   不能用作 **sql_variant** 实例的子类型。  
  
-   不支持转换或转换为 `text` 或 `ntext`。 使用`varchar(max)`或`nvarchar(max)`相反。  
  
-   不能进行比较或排序。 这意味着 `xml` 数据类型不能用在 GROUP BY 语句中。  
  
-   不能用作除 ISNULL、COALESCE 和 DATALENGTH 之外的任何内置标量函数的参数。  
  
-   不能用作索引中的键列。 但可以作为数据包含在聚集索引中；如果创建了非聚集索引，也可以使用 INCLUDE 关键字显式添加到该非聚集索引中。  
  
## <a name="see-also"></a>请参阅  
 [批量导入和导出 XML 文档的示例 (SQL Server)](../import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
