---
title: ODBC 流组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e8e6d85db11c31a8e86348b009fca06e6a2d2810
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332041"
---
# <a name="odbc-flow-components"></a>ODBC 流组件
  本主题介绍使用 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 适用于 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 的开放式数据库连接 (ODBC) 连接器有助于 SSIS 开发人员轻松创建从支持 ODBC 的数据库加载和卸载数据的包。  
  
 ODBC 连接器设计为在将数据加载到 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]的上下文中支持 ODBC 的数据库中或者从支持 ODBC 的数据库卸载数据时获得最佳性能。  
  
## <a name="benefits"></a>优势  
 用于 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 的 ODBC 源和 ODBC 目标在处理从支持 ODBC 的数据库加载数据或卸载数据方面为项目中的 SSIS 提供竞争力。  
  
 ODBC 源和 ODBC 目标实现了与支持 ODBC 的数据库的高性能数据集成。 这两个组件都可以配置为使用按行参数数组绑定来用于支持此模式的绑定的高性能 ODBC 访问接口，以及使用单行参数绑定来用于低性能的 ODBC 访问接口。  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>ODBC 源和目标入门  
 在您可以设置使用 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]的包之前，必须确保以下项可用。  
  
-   [ODBC 源](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC 目标](../../integration-services/data-flow/odbc-destination.md)  
  
 ODBC 源和 ODBC 目标提供一个简便的方法来卸载和加载数据，以及将数据从支持 ODBC 的源数据库转移到支持 ODBC 的目标数据库。  
  
 若要使用源或目标来加载或卸载数据，请在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中打开一个新的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]项目。 然后源或目标拖动到 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的设计图面上。  
  
-   ODBC 源组件从支持 ODBC 的源数据库读取数据。  
  
 不能将 ODBC 源连接到任何目标或转换 SSIS 支持的组件。  
  
 **请参阅：**  
  
 ODBC 源  
  
 ODBC 源编辑器（“连接管理器”页）  
  
 ODBC 源编辑器（“错误输出”页）  
  
-   ODBC 目标可将数据加载到支持 ODBC 的数据库中。 您可以将目标连接到任何源或转换 SSIS 支持的组件。  
  
 **请参阅：**  
  
 ODBC 目标  
  
 ODBC 目标编辑器（“连接管理器”页）  
  
 ODBC 目标编辑器（“错误输出”页）  
  
## <a name="operating-scenarios"></a>操作方案  
 本节描述了 ODBC 源和目标组件的一些主要用途。  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>将数据从 SQL Server 表大容量复制到支持 ODBC 的任何数据库表  
 可以使用组件将数据从一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中大容量复制到支持 ODBC 的单个数据库表中。  
  
 下面的示例显示如何创建一个 SSIS 数据流任务，该任务从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中提取数据并且将数据加载到 DB2 表中。  
  
-   在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中创建一个 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]项目。  
  
-   创建一个 OLE DB 连接管理器，该连接管理器连接到包含您要复制的数据的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
-   创建一个 ODBC 连接管理器，该连接管理器使用本地安装的 DB2 ODBC 驱动程序以及指向本地或远程 DB2 数据库的 DSN。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据就是从该数据库加载的。  
  
-   将一个 OLE DB 源拖到设计图面，然后对该源进行配置以便从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库以及具有要提取的数据的表获取数据。 使用您以前创建的 OLE DB 连接管理器。  
  
-   将一个 ODBC 目标拖到设计图面，将源输出连接到该 ODBC 目标，然后对该目标进行配置以便将数据加载到具有您从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库提取的数据的 DB2 表中。 使用您以前创建的 ODBC 连接管理器。  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>将数据从支持 ODBC 的数据库表大容量复制到任何 SQL Server 表  
 您可以使用组件将数据从一个或多个支持 ODBC 的数据库表大容量复制到单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库表中。  
  
 下面的示例显示如何创建一个 SSIS 数据流任务，该任务从 Sybase 数据库表中提取数据并且将数据加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库表中。  
  
-   在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中打开一个新的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   创建一个 ODBC 连接管理器，该连接管理器使用本地安装的 Sybase ODBC 驱动程序以及指向本地或远程 Sybase 数据库的 DSN。 将从该数据库中提取数据。  
  
-   创建一个 OLE DB 连接管理器，该连接管理器连接到您要加载数据的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。  
  
-   将一个 ODBC 源拖到设计图面，然后对该源进行配置以便从具有要复制的数据的 Sybase 表获取数据。 使用您以前创建的 ODBC 连接管理器。  
  
-   将一个 OLE DB 目标拖到设计图面，将源输出连接到该 OLE DB 目标，然后对该目标进行配置以便将数据加载到具有您从 Sybase 数据库提取的数据的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。 使用您以前创建的 OLE DB 连接管理器。  
  
## <a name="supported-data-types"></a>支持的数据类型  
 ODBC 大容量 SSIS 组件支持所有内置的 ODBC 数据类型，包括支持大型对象（CLOB 和 BLOB）。  
  
没有针对 ODBC 3.8 规范中所述的可扩展 C 类型的数据类型支持。下表介绍每个 ODBC SQL 类型使用的 SSIS 数据类型。 SSIS 开发人员可覆盖默认映射和为输入/输出列指定不同的 SSIS 数据类型，并且不会影响所需数据转换的性能。  
  
|ODBC SQL 类型|SSIS 数据类型|注释|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|在 ODBC 驱动程序为该 SQL 数据类型将 UNSIGNED_ATTRIBUTE 设置为 SQL_TRUE 时，SQL 数据类型将映射到 SSIS 无符号类型（DT_UI1、DT_UI2、DT_UI4、DT_UI8）。|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|在 ODBC 驱动程序为该 SQL 数据类型将 UNSIGNED_ATTRIBUTE 设置为 SQL_TRUE 时，SQL 数据类型将映射到 SSIS 无符号类型（DT_UI1、DT_UI2、DT_UI4、DT_UI8）。|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|在 ODBC 驱动程序为该 SQL 数据类型将 UNSIGNED_ATTRIBUTE 设置为 SQL_TRUE 时，SQL 数据类型将映射到 SSIS 无符号类型（DT_UI1、DT_UI2、DT_UI4、DT_UI8）。|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|在 ODBC 驱动程序为该 SQL 数据类型将 UNSIGNED_ATTRIBUTE 设置为 SQL_TRUE 时，SQL 数据类型将映射到 SSIS 无符号类型（DT_UI1、DT_UI2、DT_UI4、DT_UI8）。|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC (p,s)|DT_NUMERIC (p,s)|在 P 大于或等于 38 并且 S 大于或等于 0 且 S 小于或等于 P 时，数字数据类型将映射到 DT_NUMERIC。|  
||DT_R8|在以下至少一个条件成立时，数字数据类型将映射到 DT_R8：<br /><br />精度大于 38<br /><br />刻度小于零<br /><br />刻度大于 38<br /><br />刻度大于精度|  
||DT_CY|数字数据类型在声明为 money 数据类型时将映射到 DT_CY。|  
|SQL_DECIMAL (p,s)|DT_NUMERIC (p,s)|在 P 大于或等于 38 并且 S 大于或等于 0 且 S 小于或等于 P 时，decimal 数据类型将映射到 DT_NUMERIC。|  
||DT_R8|在以下至少一个条件成立时，decimal 数据类型将映射到 DT_R8：<br /><br />精度大于 38<br /><br />刻度小于零<br /><br />刻度大于 38<br /><br />刻度大于精度|  
||DT_CY|decimal 数据类型在声明为 money 数据类型时将映射到 DT_CY。|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|如果小数位数大于 3，则 SQL_TIMESTAMP 数据类型将映射到 DT_DBTIMESTAMP2。 在所有其他情况下，它们将映射到 DT_DBTIMESTAMP。|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|如果列长度小于或等于 8000，并且 **ExposeStringsAsUnicode** 属性为 false，则使用 DT_STR。<br /><br />如果列长度小于或等于 8000，并且 **ExposeStringsAsUnicode** 属性为 false，则使用 DT_WSTR。<br /><br />如果列长度大于 8000，并且 **ExposeStringsAsUnicode** 属性为 false，则使用 DT_TEXT。<br /><br />如果列长度大于 8000，并且 **ExposeStringsAsUnicode** 属性为 true，则使用 DT_NTEXT。|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|如果 **ExposeStringsAsUnicode** 属性为 true，则使用 DT_NTEXT。|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|如果列长度小于或等于 4000，则使用 DT_WSTR。<br /><br />如果列长度大于 4000，则使用 DT_NTEXT。|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|如果列长度小于或等于 8000，则使用 DT_BYTES。<br /><br />如果列长度大于 8000，则使用 DT_IMAGE。|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|访问接口特定的数据类型|DT_BYTES<br /><br />DT_IMAGE|如果列长度小于或等于 8000，则使用 DT_BYTES。<br /><br />如果列长度为零或大于 8000，则使用 DT_IMAGE。|  
  
## <a name="in-this-section"></a>本节内容  
  
-   [ODBC 源](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC 目标](../../integration-services/data-flow/odbc-destination.md)  
  
 
