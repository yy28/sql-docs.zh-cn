---
title: 使用用户定义类型 |Microsoft 文档
description: 用于 SQL Server 用户定义的类型与 OLE DB 驱动程序
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [OLE DB Driver for SQL Server]
- user-defined types [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- MSOLEDBSQL, user-defined types
- OLE DB Driver for SQL Server, user-defined types
- data access [OLE DB Driver for SQL Server], user-defined types
- ISSCommandWithParameters interface
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab7235c1b9f1bd9155fc949df39c2b0995ba0b63
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="using-user-defined-types"></a>使用用户定义类型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 介绍了用户定义类型 (UDT)。 Udt 扩展，它允许你存储对象和自定义数据结构中的 SQL 类型系统[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。 UDT 可以包含多种数据类型并且可具有行为，这使它们不同于由单一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统数据类型构成的传统别名数据类型。 使用生成可验证代码的 .NET 公共语言运行时 (CLR) 所支持的任何语言都可以定义 UDT， 这包括 Microsoft Visual C#<sup>®</sup>和 Visual Basic<sup>®</sup> .NET。 数据公开为 .NET 类或结构的字段和属性，行为则由类或结构的方法来定义。  
  
 UDT 可以用作表的列定义为中的变量[!INCLUDE[tsql](../../../includes/tsql-md.md)]批处理，或作为自变量的[!INCLUDE[tsql](../../../includes/tsql-md.md)]函数或存储的过程。  
  
## <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序  
 SQL Server 的 OLE DB 驱动程序支持 Udt 作为具有允许你管理 Udt 作为对象的元数据信息的二进制类型。 作为以外，dbtype_udt 还，公开 UDT 列，通过核心 OLE DB 接口公开其元数据**IColumnRowset**，并且新[ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)接口。  
  
> [!NOTE]  
>  **IRowsetFind::FindNextRow**方法并不适用于 UDT 数据类型。 如果将 UDT 用作搜索列类型，则返回 DB_E_BADCOMPAREOP。  
  
### <a name="data-bindings-and-coercions"></a>数据绑定和强制  
 下表说明将所列数据类型与某一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UDT 一同使用时出现的绑定和强制。 UDT 列作为以外，dbtype_udt 还公开通过 OLE DB 驱动程序的 SQL Server。 可以通过适当的架构行集获取元数据，这样即可将您自行定义的类型作为对象来管理。  
  
|数据类型|到服务器<br /><br /> **UDT**|到服务器<br /><br /> **non-UDT**|从服务器<br /><br /> **UDT**|从服务器<br /><br /> **non-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|支持<sup>6</sup>|错误<sup>1</sup>|支持<sup>6</sup>|Error<sup>5</sup>|  
|DBTYPE_BYTES|支持<sup>6</sup>|N/A<sup>2</sup>|支持<sup>6</sup>|N/A<sup>2</sup>|  
|DBTYPE_WSTR|支持<sup>3,6</sup>|N/A<sup>2</sup>|支持<sup>4,6</sup>|N/A<sup>2</sup>|  
|DBTYPE_BSTR|支持<sup>3,6</sup>|N/A<sup>2</sup>|支持<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_STR|支持<sup>3,6</sup>|N/A<sup>2</sup>|支持<sup>4,6</sup>|N/A<sup>2</sup>|  
|DBTYPE_IUNKNOWN|不支持|N/A<sup>2</sup>|不支持|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|支持<sup>6</sup>|N/A<sup>2</sup>|支持<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|支持<sup>3,6</sup>|N/A<sup>2</sup>|N/A|N/A<sup>2</sup>|  
  
 <sup>1</sup>如果服务器的类型是其他比以外，dbtype_udt 还指定使用**ICommandWithParameters::SetParameterInfo**和访问器类型是以外，dbtype_udt 还，执行语句时出错 (DB_E_ERRORSOCCURRED;参数状态是 DBSTATUS_E_BADACCESSOR）。 如果不是这样，数据将发送到服务器，但服务器会返回错误，指示不存在从 UDT 到参数的数据类型的隐式转换。  
  
 <sup>2</sup>超出本文的范围。  
  
 <sup>3</sup>从十六进制字符串到二进制数据的数据转换出现。  
  
 <sup>4</sup>从二进制数据以十六进制字符串数据转换出现。  
  
 <sup>5</sup>创建访问器时，或者在提取时，该错误是 DB_E_ERRORSOCCURRED，绑定设置为 DBBINDSTATUS_UNSUPPORTEDCONVERSION 的状态，可以在进行验证。  
  
 <sup>6</sup>BY_REF 可能会使用。  
  
 可以绑定 DBTYPE_NULL 和 DBTYPE_EMPTY，用于输入参数，但不是能为输出参数或结果。 为输入参数进行绑定时，状态必须设置为 DBSTATUS_S_ISNULL 或 DBSTATUS_S_DEFAULT。  
  
 还可以将 DBTYPE_UDT 转换为 DBTYPE_EMPTY 和 DBTYPE_NULL，但无法将 DBTYPE_NULL 和 DBTYPE_EMPTY 转换为 DBTYPE_UDT。 这与 DBTYPE_BYTES 的情况是一致的。  
  
> [!NOTE]  
>  新接口用于处理作为参数，Udt **ISSCommandWithParameters**，它继承自**ICommandWithParameters**。 应用程序必须使用此接口为 UDT 参数至少设置 DBPROPSET_SQLSERVERPARAMETER 属性集的 SSPROP_PARAM_UDT_NAME。 如果不执行此操作， **ICommand::Execute**将返回 DB_E_ERRORSOCCURRED。 此文章的更高版本中介绍了此接口和属性集。  
  
 如果不是大到足以保留所有数据，列中插入的用户定义的类型**ICommand::Execute**将返回的状态为 DB_E_ERRORSOCCURRED，则为 S_OK。  
  
 OLE DB 核心服务提供的数据转换 (**IDataConvert**) 不适用于以外，dbtype_udt 还。 不支持其他绑定。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 行集的添加和更改内容  
 OLE DB 驱动程序的 SQL Server 添加新值，或更改到多个核心 OLE DB 架构行集。  
  
#### <a name="the-procedureparameters-schema-rowset"></a>PROCEDURE_PARAMETERS 架构行集  
 在 PROCEDURE_PARAMETERS 架构行集中添加了以下内容。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|由三部分组成的名称标识符。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|由三部分组成的名称标识符。|  
|SS_UDT_NAME|DBTYPE_WSTR|由三部分组成的名称标识符。|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|程序集限定名称，包括类型名称和所有必要引用的 CLR 的程序集标识。|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>SQL_ASSEMBLIES 架构行集  
 SQL Server 的 OLE DB 驱动程序公开描述已注册的 Udt 的新提供程序特定的架构行集。 可以将 ASSEMBLY 服务器指定为 DBTYPE_WSTR，但它在行集中不存在。 如果未指定，行集将默认使用当前服务器。 下表中定义 SQL_ASSEMBLIES 架构行集：  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|包含该类型的程序集的目录名称。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|包含该类型的程序集的架构名称或所有者名称。 尽管程序集的作用域为数据库而不是架构，但它们仍具有在此所反映的所有者。|  
|ASSEMBLY_NAME|DBTYPE_WSTR|包含该类型的程序集的名称。|  
|ASSEMBLY_ID|DBTYPE_UI4|包含类型的程序集对象 ID。|  
|PERMISSION_SET|DBTYPE_WSTR|指示程序集的访问范围的值。 这些值包括“SAFE”、“EXTERNAL_ACCESS”和“UNSAFE”。|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|程序集的二进制表示形式。|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>SQL_ASSEMBLIES_ DEPENDENCIES 架构行集  
 OLE DB 驱动程序的 SQL Server 公开描述指定的服务器的程序集依赖项的新提供程序特定的架构行集。 ASSEMBLY_SERVER 可由调用方指定为 DBTYPE_WSTR，但在该行集中不存在。 如果未指定，行集将默认使用当前服务器。 下表中定义 SQL_ASSEMBLY_DEPENDENCIES 架构行集：  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|包含该类型的程序集的目录名称。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|包含该类型的程序集的架构名称或所有者名称。 尽管由数据库而不是架构的应用范围限定程序集，它们仍有一个所有者，此处反映。|  
|ASSEMBLY_ID|DBTYPE_UI4|程序集的对象 ID。|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|引用的程序集的对象 ID。|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>SQL_USER_TYPES 架构行集  
 OLE DB 驱动程序的 SQL Server 显示新架构行集，SQL_USER_TYPES，描述指定服务器已注册的 Udt 添加中时。 UDT_SERVER 必须由调用方指定为 DBTYPE_WSTR，但它在该行集中不存在。 在下表中定义 SQL_USER_TYPES 架构行集。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，指定目录的名称在其中定义用户定义的类型。|  
|UDT_SCHEMANAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，指定在其中定义用户定义的类型的架构的名称。|  
|UDT_NAME|DBTYPE_WSTR|包含 UDT 类的程序集的名称。|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|完整类型名称 (AQN) 包括带有命名空间前缀（如果适用）的类型名称。|  
  
#### <a name="the-columns-schema-rowset"></a>COLUMNS 架构行集  
 添加对所列架构行集包括以下各列：  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，指定目录的名称在其中定义用户定义的类型。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，指定在其中定义用户定义的类型的架构的名称。|  
|SS_UDT_NAME|DBTYPE_WSTR|UDT 的名称|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|完整类型名称 (AQN) 包括带有命名空间前缀（如果适用）的类型名称。|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB 属性集的添加和更改内容  
 OLE DB 驱动程序的 SQL Server 添加新值，或更改到多个核心 OLE DB 属性集。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 属性集  
 为了支持通过 OLE DB 的 Udt，OLE DB 驱动程序的 SQL Server 实现新的 DBPROPSET_SQLSERVERPARAMETER 属性集，其中包含以下值：  
  
|名称|类型|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|由三部分组成的名称标识符。<br /><br /> 对于 UDT 参数，此属性是一个字符串，它指定定义用户定义类型的目录的名称。|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|由三部分组成的名称标识符。<br /><br /> 对于 UDT 参数，此属性是一个字符串，它指定定义用户定义类型的架构的名称。|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|由三部分组成的名称标识符。<br /><br /> 对于 UDT 列，此属性是一个字符串，它指定仅由一个部分组成的用户定义类型名称。|  
  
 SSPROP_PARAM_UDT_NAME 是必需的。 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME 是可选的。 如果未正确指定了任何属性，将返回 DB_E_ERRORSINCOMMAND。 如果未指定 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME，则必须在定义表的同一数据库和架构中定义 UDT。 如果 UDT 定义没有位于表所在的架构中（但位于相同的数据库中），则必须指定 SSPROP_PARAM_UDT_SCHEMANAME。 如果在不同数据库中有 UDT 定义，则必须指定 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME。  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 属性集  
 若要支持中的表创建**ITableDefinition**接口，OLE DB 驱动程序的 SQL Server 将以下三个新列添加到 DBPROPSET_SQLSERVERCOLUMN 属性集。  
  
|名称|Description|类型|Description|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|对于 DBTYPE_UDT 类型的列，此属性是一个字符串，它指定定义 UDT 的目录的名称。|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|对于 DBTYPE_UDT 类型的列，此属性是一个字符串，它指定定义 UDT 的架构的名称。|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|对于 DBTYPE_UDT 类型的列，此属性是一个字符串，它指定仅由一个部分组成的 UDT 名称。 对于其他列类型，此属性返回一个空字符串。|  
  
> [!NOTE]  
>  UDT 不出现在 PROVIDER_TYPES 架构行集中。 所有列都具有读写访问权限。  
  
 ADO 将通过使用“说明”列中的相应条目引用这些属性。  
  
 SSPROP_COL_UDTNAME 是必需的。 SSPROP_COL_UDT_CATALOGNAME 和 SSPROP_COL_UDT_SCHEMANAME 是可选的。 如果不正确地指定任何属性**DB_E_ERRORSINCOMMAND**将返回。  
  
 如果既未指定 SSPROP_COL_UDT_CATALOGNAME 也未指定 SSPROP_COL_UDT_SCHEMANAME，则必须在定义表的同一数据库和架构中定义 UDT。  
  
 如果 UDT 定义没有与表位于同一架构中（但位于同一数据库中），则必须指定 SSPROP_COL_UDT_SCHEMANAME。  
  
 如果 UDT 定义位于不同的数据库中，则必须指定 SSPROP_COL_UDT_CATALOGNAME 和 SSPROP_COL_UDT_SCHEMANAME。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 接口的添加和更改内容  
 OLE DB 驱动程序的 SQL Server 添加新值，或到多个 OLE DB 接口的核心更改。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 接口  
 若要支持通过 OLE DB 的 Udt，OLE DB 驱动程序的 SQL Server 实现大量更改，包括添加**ISSCommandWithParameters**接口。 此新接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了从继承的三个方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供**GetParameterProperties**和**SetParameterProperties**习惯于句柄服务器特定的方法数据类型。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**接口还可以使用新 SSPARAMPROPS 的结构。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 接口  
 除了**ISSCommandWithParameters**接口，OLE DB 驱动程序用于 SQL Server 还将新值添加到从调用返回的行集**IColumnsRowset::GetColumnRowset**方法包括以下。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 目录名称标识符。|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 架构名称标识符。|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|UDT 名称标识符。|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|程序集限定名，其中包括 CLR 引用所需的类型名称和所有程序集标识。|  
  
 在 DBCOLUMN_TYPE 设置为以外，dbtype_udt 还通过查看前面的表中指定的添加 UDT 元数据时，你可以从其他二进制类型区分服务器 UDT 列。 如果该数据不完整，服务器类型为 UDT。 对于非 UDT 服务器类型，这些列的返回结果始终为 NULL。  
 
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
