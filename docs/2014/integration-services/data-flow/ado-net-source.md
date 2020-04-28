---
title: ADO NET 源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 296163b64d565ae3a65a16f1dbbf002bfc464bee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70153962"
---
# <a name="ado-net-source"></a>ADO NET 源
  ADO NET 源使用来自 .NET 提供程序的数据，并使这些数据对数据流可用。  
  
 可使用 ADO NET 源连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 不支持使用 OLE DB 连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 有关 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的详细信息，请参阅[通用指导原则和限制（Azure SQL 数据库）](https://go.microsoft.com/fwlink/?LinkId=248228)。  
  
## <a name="data-type-support"></a>数据类型支持  
 源会将未映射到特定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的任意数据类型转换为 DT_NTEXT [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 即使数据类型为 `System.Object`，也会发生此转换。  
  
 可以将 DT_NTEXT 数据类型更改为 DT_WSTR 数据类型，也可以将 DT_WSTR 更改为 DT_NTEXT。 通过在 ADO NET 源的 **“高级编辑器”** 对话框中设置 **DataType** 属性可更改数据类型。 有关详细信息，请参阅 [Common Properties](../common-properties.md)。  
  
 通过在 ADO NET 源之后使用数据转换，还可以将 DT_NTEXT 数据类型转换为 DT_BYTES 或 DT_STR 数据类型。 有关详细信息，请参阅 [Data Conversion Transformation](transformations/data-conversion-transformation.md)。  
  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，日期数据类型 DT_DBDATE、DT_DBTIME2、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的某些日期数据类型。 您可以配置 ADO NET 源，从而将日期数据类型从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的数据类型转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用的数据类型。 若要配置 ADO NET 源以便转换这些日期数据类型，请将 **连接管理器的** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 属性设置为 **Latest**。 （**Type System Version** 属性位于“连接管理器”  对话框的“全部”  页。 若要打开“连接管理器”  对话框，请右键单击 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器，然后单击“编辑”  。  
  
> [!NOTE]  
>  如果将 **连接管理器的** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 属性设置为 **SQL Server 2005**，则系统会将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期数据类型转换为 DT_WSTR。  
  
 当 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 连接管理器将提供程序指定为 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) 时，系统会将用户定义的数据类型 (UDT) 转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 二进制大型对象 (BLOB)。 当系统转换 UDT 数据类型时会应用下列规则：  
  
-   如果数据是非大型 UDT，系统会将该数据转换为 DT_BYTES。  
  
-   如果数据是非大型 UDT，并且数据库中列的 **Length** 属性设置为 -1 或大于 8,000 个字节的值，则系统会将该数据转换为 DT_IMAGE。  
  
-   如果数据是大型 UDT，系统会将该数据转换为 DT_IMAGE。  
  
    > [!NOTE]  
    >  如果 ADO NET 源未配置为使用错误输出，则系统会以 8,000 个字节为单位成块地使数据流向 DT_IMAGE 列。 如果 ADO NET 源配置为使用错误输出，则系统会将整个字节数组传递到 DT_IMAGE 列。 有关如何将组件配置为使用错误输出的详细信息，请参阅 [数据中的错误处理](error-handling-in-data.md)。  
  
 有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型、支持的数据类型转换以及某些数据库（包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）之间的数据类型映射的详细信息，请参阅 [Integration Services 数据类型](integration-services-data-types.md)。  
  
 有关将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型映射为托管数据类型的详细信息，请参阅 [在数据流中使用数据类型](../extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)。  
  
## <a name="ado-net-source-troubleshooting"></a>ADO NET 源故障排除  
 可以记录 ADO NET 源对外部数据访问接口所做的调用。 利用此日志记录功能，可以对 ADO NET 源执行的从外部数据源加载数据的操作进行故障排除。 若要记录 ADO NET 源对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="ado-net-source-configuration"></a>ADO NET 源配置  
 通过提供定义结果集的 SQL 语句可以配置 ADO NET 源。 例如，连接到 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 数据库并使用 SQL 语句 `SELECT * FROM Production.Product` 的 ADO NET 源可从 **Production.Product** 表提取所有行，并将数据集提供给下游组件。  
  
> [!NOTE]  
>  在您使用 SQL 语句调用从临时表返回结果的某一存储过程时，使用 WITH RESULT SETS 选项可为结果集定义元数据。  
  
> [!NOTE]  
>  如果使用 SQL 语句来执行存储过程且包因为以下错误失败，您可以通过在 exec 语句前添加 `SET FMTONLY OFF` 语句来更正错误。  
>   
>  **在数据源中找不到列 <列名>。**  
  
 ADO NET 源使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器连接到数据源，该连接管理器指定 .NET 提供程序。 有关详细信息，请参阅 [ADO.NET Connection Manager](../connection-manager/ado-net-connection-manager.md)。  
  
 ADO NET 源有一个常规输出和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
-   [ADO NET 自定义属性](ado-net-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另请参阅  
 [DataReader 目标](datareader-destination.md)   
 [ADO NET 目标](ado-net-destination.md)   
 [数据流](data-flow.md)  
  
  
