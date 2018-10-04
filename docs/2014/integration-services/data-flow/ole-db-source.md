---
title: OLE DB 源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsource.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1b1d37bba3216a22d732c5562108db51925d37bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120574"
---
# <a name="ole-db-source"></a>OLE DB 源
  OLE DB 源通过使用数据库表、视图或 SQL 命令，从各种兼容 OLE DB 的关系数据库中提取数据。 例如，OLE DB 源可以从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表中提取数据。  
  
 OLE DB 源提供四种不同数据访问模式用于提取数据：  
  
-   表或视图。  
  
-   变量中指定的表或视图。  
  
-   SQL 语句的运行结果。 查询可以是参数化查询。  
  
-   存储在变量中的 SQL 语句的运行结果。  
  
> [!NOTE]  
>  在您使用 SQL 语句调用从临时表返回结果的某一存储过程时，使用 WITH RESULT SETS 选项可为结果集定义元数据。  
  
 如果使用参数化查询，则可以将变量映射到参数，以便在 SQL 语句中指定单个参数的值。  
  
 这个源使用 OLE DB 连接管理器连接到数据源，而该连接管理器则指定要使用的 OLE DB 访问接口。 有关详细信息，请参阅 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目也提供可据以创建 OLE DB 连接管理器的数据源对象，从而使 OLE DB 源可以使用数据源和数据源视图。  
  
 根据不同的 OLE DB 访问接口，对 OLE DB 源存在一些限制：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle 不支持 Oracle 数据类型 BLOB、CLOB、NCLOB、BFILE 或 UROWID，因此，OLE DB 源不能从包含这些数据类型列的表中提取数据。  
  
-   IBM OLE DB DB2 访问接口和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 访问接口不支持使用调用存储过程的 SQL 命令。 如果使用这种命令，OLE DB 源将无法创建列元数据，这样一来，数据流中 OLE DB 源之后的数据流组件将没有可用的列数据，从而导致数据流执行失败。  
  
 OLE DB 源有一个常规输出和一个错误输出。  
  
## <a name="using-parameterized-sql-statements"></a>使用参数化 SQL 语句  
 OLE DB 源可以使用 SQL 语句来提取数据。 此语句可以是 SELECT 或 EXEC 语句。  
  
 OLE DB 源使用 OLE DB 连接管理器来连接到它从中提取数据的数据源。 取决于 OLE DB 连接管理器所使用的访问接口和连接管理器所连接的关系数据库管理系统 (RDBMS)，参数的命名和列出将应用不同的规则。 如果参数名是从 RDBMS 返回的，则可以使用参数名来将参数列表中的参数映射到 SQL 语句中的参数；否则，参数将按它们在参数列表中的序数位置映射到 SQL 语句中的参数。 支持的参数名类型按访问接口而各不相同。 例如，某些访问接口要求使用变量或列名称，而某些访问接口则要求使用诸如 0 或 Param0 这样的符号名称。 应当参阅访问接口对应的文档，了解有关在 SQL 语句中使用的参数名称的信息。  
  
 使用 OLE DB 连接管理器时，不能使用参数化子查询，这是因为 OLE DB 源不能通过 OLE DB 访问接口派生参数信息。 但是，可以使用表达式将参数值连接到查询字符串并设置该源的 SqlCommand 属性。在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，可以使用“OLE DB 源编辑器”对话框配置 OLE DB 源，并在“设置查询参数”对话框中将参数映射到变量。  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>使用序号位置指定参数  
 如果没有返回参数名，则 **“设置查询参数”** 对话框中的 **“参数”** 列表中的参数列出顺序将控制运行时参数将映射哪个参数标记。 列表中的第一个参数将映射到 SQL 语句中的第一个 ?， 第二个参数映射到第二个 ?，以此类推。  
  
 以下 SQL 语句选择 **数据库的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 表中的行。 **Mappings** 列表中的第一个参数映射到 **Color** 列的第一个参数，第二个参数映射到 **Size** 列。  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 参数名不受影响。 例如，如果参数与它所应用的列同名，但在 **“参数”** 列表中没有放在正确的序号位置，则在运行时发生的参数映射将使用参数的序号位置，而不是参数名称。  
  
 EXEC 命令通常要求在过程中使用提供参数值的变量的名称作为参数名称。  
  
### <a name="specifying-parameters-by-using-names"></a>使用名称来指定参数  
 如果实际参数名称是从 RDBMS 返回的，则 SELECT 和 EXEC 语句所使用的参数将按名称进行映射。 参数名称必须与存储过程（由 SELECT 语句或 EXEC 语句运行）所期望的名称匹配。  
  
 以下 SQL 语句运行 **uspGetWhereUsedProductID** 存储过程（在 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 数据库中可用）。  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 存储过程希望变量 `@StartProductID` 和 `@CheckDate`提供参数值。 参数出现在 **“映射”** 列表中的顺序是不相关的。 唯一要求是，参数名必须与存储过程中的变量名一致，包括 \@ 符号在内。  
  
### <a name="mapping-parameters-to-variables"></a>将参数映射到变量  
 在运行时参数将映射到提供参数值的变量。 尽管也可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的系统变量，但变量通常是用户定义变量。 如果使用用户定义变量，请确保将数据类型设置为与映射参数所引用的列的数据类型相兼容的类型。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)。  
  
## <a name="troubleshooting-the-ole-db-source"></a>OLE DB 源故障排除  
 可以记录 OLE DB 源对外部数据访问接口所做的调用。 利用此日志记录功能，可以对 OLE DB 源执行的从外部数据源加载数据的操作进行故障排除。 若要记录 OLE DB 源对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-source"></a>配置 OLE DB 源  
 可以采用编程方式或通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。  
  
 有关可以在 **“OLE DB 源编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [OLE DB 源编辑器&#40;连接管理器页&#41;](../ole-db-source-editor-connection-manager-page.md)  
  
-   [OLE DB 源编辑器&#40;列页&#41;](../ole-db-source-editor-columns-page.md)  
  
-   [OLE DB 源编辑器&#40;错误输出页&#41;](../ole-db-source-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
-   [OLE DB 自定义属性](ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [使用 OLE DB 源提取数据](ole-db-source.md)  
  
-   [将查询参数映射到数据流组件中的变量](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>相关内容  
 social.technet.microsoft.com 上的 Wiki 文章 [SSIS 与 Oracle 连接器](http://go.microsoft.com/fwlink/?LinkId=220670)。  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 目标](ole-db-destination.md)   
 [Integration Services &#40;SSIS&#41;变量](../integration-services-ssis-variables.md)   
 [数据流](data-flow.md)  
  
  
