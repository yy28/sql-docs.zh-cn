---
title: 使用用户定义类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [SQL Server Native Client]
- user-defined types [SQL Server], SQL Server Native Client
- SQL Server Native Client OLE DB provider, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- SQLNCLI, user-defined types
- SQL Server Native Client, user-defined types
- data access [SQL Server Native Client], user-defined types
- ISSCommandWithParameters interface
ms.assetid: e15d8169-3517-4323-9c9e-0f5c34aff7df
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eef3d47ae77c8686ce09eb77665e64de53a229ce
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424796"
---
# <a name="using-user-defined-types"></a>使用用户定义类型
[!INCLUDE[appliesto-ss-asdb-xxxx-pdw-md](../../../includes/appliesto-ss-asdb-xxxx-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 介绍了用户定义类型 (UDT)。 Udt 允许您存储对象和自定义数据结构中的扩展了 SQL 类型系统[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。 UDT 可以包含多种数据类型并且可具有行为，这使它们不同于由单一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统数据类型构成的传统别名数据类型。 使用生成可验证代码的 .NET 公共语言运行时 (CLR) 所支持的任何语言都可以定义 UDT， 这包括 Microsoft Visual C#<sup>®</sup>和 Visual Basic<sup>®</sup> .NET。 数据公开为 .NET 类或结构的字段和属性，行为则由类或结构的方法来定义。  
  
 UDT 可用作表的列定义中的变量[!INCLUDE[tsql](../../../includes/tsql-md.md)]批处理，或作为自变量的[!INCLUDE[tsql](../../../includes/tsql-md.md)]函数或存储的过程。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 访问接口  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持 Udt 作为带有元数据信息，允许你管理 Udt 作为对象的二进制类型。 UDT 列公开为 DBTYPE_UDT，并通过核心 OLE DB 接口公开其元数据**IColumnRowset**，并且新[ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)接口。  
  
> [!NOTE]  
>  **Irowsetfind:: Findnextrow**方法并不适用于 UDT 数据类型。 如果将 UDT 用作搜索列类型，则返回 DB_E_BADCOMPAREOP。  
  
### <a name="data-bindings-and-coercions"></a>数据绑定和强制  
 下表说明将所列数据类型与某一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UDT 一同使用时出现的绑定和强制。 通过公开 UDT 列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序为 DBTYPE_UDT。 可以通过适当的架构行集获取元数据，这样即可将您自行定义的类型作为对象来管理。  
  
|数据类型|到服务器<br /><br /> **UDT**|到服务器<br /><br /> **non-UDT**|从服务器<br /><br /> **UDT**|从服务器<br /><br /> **non-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|支持<sup>6</sup>|错误<sup>1</sup>|支持<sup>6</sup>|错误<sup>5</sup>|  
|DBTYPE_BYTES|支持<sup>6</sup>|N/A<sup>2</sup>|支持<sup>6</sup>|N/A<sup>2</sup>|  
|DBTYPE_WSTR|支持<sup>3,6</sup>|N/A<sup>2</sup>|支持<sup>4,6</sup>|N/A<sup>2</sup>|  
|DBTYPE_BSTR|支持<sup>3,6</sup>|N/A<sup>2</sup>|支持<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_STR|支持<sup>3,6</sup>|N/A<sup>2</sup>|支持<sup>4,6</sup>|N/A<sup>2</sup>|  
|DBTYPE_IUNKNOWN|不支持|N/A<sup>2</sup>|不支持|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &AMP;#124; VT_ARRAY)|支持<sup>6</sup>|N/A<sup>2</sup>|支持<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|支持<sup>3,6</sup>|N/A<sup>2</sup>|N/A|N/A<sup>2</sup>|  
  
 <sup>1</sup>如果的服务器类型与指定了 DBTYPE_UDT 之外**icommandwithparameters:: Setparameterinfo**取值函数类型为 DBTYPE_UDT，执行该语句时出错 (DB_E_ERRORSOCCURRED;参数状态为 DBSTATUS_E_BADACCESSOR）。 如果不是这样，数据将发送到服务器，但服务器会返回错误，指示不存在从 UDT 到参数的数据类型的隐式转换。  
  
 <sup>2</sup>超出了本主题的范围。  
  
 <sup>3</sup>从十六进制字符串到二进制数据的数据转换时发生。  
  
 <sup>4</sup>从二进制数据为十六进制字符串转换。  
  
 <sup>5</sup>验证可以会在创建取值函数时或在提取时，错误为 DB_E_ERRORSOCCURRED，绑定状态设置为 DBBINDSTATUS_UNSUPPORTEDCONVERSION。  
  
 <sup>6</sup>可能会使用 BY_REF。  
  
 可以绑定 DBTYPE_NULL 和 DBTYPE_EMPTY，用于输入参数而不是输出参数或结果。 为输入参数进行绑定时，状态必须设置为 DBSTATUS_S_ISNULL 或 DBSTATUS_S_DEFAULT。  
  
 还可以将 DBTYPE_UDT 转换为 DBTYPE_EMPTY 和 DBTYPE_NULL，但无法将 DBTYPE_NULL 和 DBTYPE_EMPTY 转换为 DBTYPE_UDT。 这与 DBTYPE_BYTES 的情况是一致的。  
  
> [!NOTE]  
>  用于处理 Udt 作为参数，使用新接口**ISSCommandWithParameters**，后者又继承**ICommandWithParameters**。 应用程序必须使用此接口为 UDT 参数至少设置 DBPROPSET_SQLSERVERPARAMETER 属性集的 SSPROP_PARAM_UDT_NAME。 如果不执行此操作， **icommand:: Execute**将返回 DB_E_ERRORSOCCURRED。 此接口和属性集将在本主题的下文中介绍。  
  
 如果用户定义类型插入到不是大到足以保留其所有数据的列**icommand:: Execute**将返回 S_OK，且状态为 DB_E_ERRORSOCCURRED。  
  
 OLE DB 核心服务提供的数据转换 (**IDataConvert**) 不适用于 DBTYPE_UDT。 不支持其他绑定。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 行集的添加和更改内容  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端添加了新值，或将更改为许多核心 OLE DB 架构行集。  
  
#### <a name="the-procedureparameters-schema-rowset"></a>PROCEDURE_PARAMETERS 架构行集  
 在 PROCEDURE_PARAMETERS 架构行集中添加了以下内容。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|由三部分组成的名称标识符。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|由三部分组成的名称标识符。|  
|SS_UDT_NAME|DBTYPE_WSTR|由三部分组成的名称标识符。|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|程序集限定名称，其中包括类型名称和由 CLR 引用所需的所有程序集标识。|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>SQL_ASSEMBLIES 架构行集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开描述的已注册的 Udt 的新提供程序特定的架构行集。 可以将 ASSEMBLY 服务器指定为 DBTYPE_WSTR，但它在行集中不存在。 如果未指定，行集将默认使用当前服务器。 下表中定义了 SQL_ASSEMBLIES 架构行集。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|包含该类型的程序集的目录名称。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|包含该类型的程序集的架构名称或所有者名称。 尽管程序集的作用域为数据库而不是架构，但它们仍具有在此所反映的所有者。|  
|ASSEMBLY_NAME|DBTYPE_WSTR|包含该类型的程序集的名称。|  
|ASSEMBLY_ID|DBTYPE_UI4|包含该类型的程序集的对象 ID。|  
|PERMISSION_SET|DBTYPE_WSTR|指示程序集的访问范围的值。 这些值包括“SAFE”、“EXTERNAL_ACCESS”和“UNSAFE”。|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|程序集的二进制表示形式。|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>SQL_ASSEMBLIES_ DEPENDENCIES 架构行集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开描述指定的服务器的程序集依赖关系的新提供程序特定的架构行集。 ASSEMBLY_SERVER 可由调用方指定为 DBTYPE_WSTR，但在该行集中不存在。 如果未指定，行集将默认使用当前服务器。 SQL_ASSEMBLY_DEPENDENCIES 架构行集在下表中定义。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|包含该类型的程序集的目录名称。|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|包含该类型的程序集的架构名称或所有者名称。 虽然数据库而不是架构，程序集的作用域，但是它们仍需要所反映的所有者。|  
|ASSEMBLY_ID|DBTYPE_UI4|程序集的对象 ID。|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|所引用的程序集的对象 ID。|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>SQL_USER_TYPES 架构行集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开新架构行集 SQL_USER_TYPES，描述何时添加指定的服务器的已注册的 Udt。 UDT_SERVER 必须由调用方指定为 DBTYPE_WSTR，但它在该行集中不存在。 在下表中定义 SQL_USER_TYPES 架构行集。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，它指定定义 UDT 的目录的名称。|  
|UDT_SCHEMANAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，它指定定义 UDT 的架构的名称。|  
|UDT_NAME|DBTYPE_WSTR|包含 UDT 类的程序集的名称。|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|完整类型名称 (AQN) 包括带有命名空间前缀（如果适用）的类型名称。|  
  
#### <a name="the-columns-schema-rowset"></a>COLUMNS 架构行集  
 COLUMNS 架构行集添加了以下列。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，它指定定义 UDT 的目录的名称。|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|对于 UDT 列，此属性是一个字符串，它指定定义 UDT 的架构的名称。|  
|SS_UDT_NAME|DBTYPE_WSTR|UDT 的名称|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|完整类型名称 (AQN) 包括带有命名空间前缀（如果适用）的类型名称。|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB 属性集的添加和更改内容  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端添加了新值或更改为许多核心 OLE DB 属性集。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 属性集  
 若要通过 OLE DB 支持 Udt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 实现新的 DBPROPSET_SQLSERVERPARAMETER 属性集包含以下值。  
  
|“属性”|类型|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|由三部分组成的名称标识符。<br /><br /> 对于 UDT 参数，此属性是一个字符串，它指定定义用户定义类型的目录的名称。|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|由三部分组成的名称标识符。<br /><br /> 对于 UDT 参数，此属性是一个字符串，它指定定义用户定义类型的架构的名称。|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|由三部分组成的名称标识符。<br /><br /> 对于 UDT 列，此属性是一个字符串，它指定仅由一个部分组成的用户定义类型名称。|  
  
 SSPROP_PARAM_UDT_NAME 是必需的。 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME 是可选的。 如果任何属性指定有误，将返回 DB_E_ERRORSINCOMMAND。 如果未指定 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME，则必须在定义表的同一数据库和架构中定义 UDT。 如果 UDT 定义没有位于表所在的架构中（但位于相同的数据库中），则必须指定 SSPROP_PARAM_UDT_SCHEMANAME。 如果 UDT 定义位于不同的数据库中，则必须指定 SSPROP_PARAM_UDT_CATALOGNAME 和 SSPROP_PARAM_UDT_SCHEMANAME。  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 属性集  
 若要支持中的表创建**ITableDefinition**接口， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 向 DBPROPSET_SQLSERVERCOLUMN 属性集添加以下三个新列。  
  
|“属性”|Description|类型|Description|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|对于 DBTYPE_UDT 类型的列，此属性是一个字符串，它指定定义 UDT 的目录的名称。|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|对于 DBTYPE_UDT 类型的列，此属性是一个字符串，它指定定义 UDT 的架构的名称。|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|对于 DBTYPE_UDT 类型的列，此属性是一个字符串，它指定仅由一个部分组成的 UDT 名称。 对于其他列类型，此属性返回空字符串。|  
  
> [!NOTE]  
>  UDT 不出现在 PROVIDER_TYPES 架构行集中。 所有列都具有读写访问权限。  
  
 ADO 将通过使用“说明”列中的相应条目引用这些属性。  
  
 SSPROP_COL_UDTNAME 是必需的。 SSPROP_COL_UDT_CATALOGNAME 和 SSPROP_COL_UDT_SCHEMANAME 是可选的。 如果任何属性的指定了不正确地**DB_E_ERRORSINCOMMAND**将返回。  
  
 如果既未指定 SSPROP_COL_UDT_CATALOGNAME 也未指定 SSPROP_COL_UDT_SCHEMANAME，则必须在定义表的同一数据库和架构中定义 UDT。  
  
 如果 UDT 定义没有与表位于同一架构中（但位于同一数据库中），则必须指定 SSPROP_COL_UDT_SCHEMANAME。  
  
 如果 UDT 定义位于不同的数据库中，则必须指定 SSPROP_COL_UDT_CATALOGNAME 和 SSPROP_COL_UDT_SCHEMANAME。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 接口的添加和更改内容  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 本机客户端添加了新值，或将更改为许多核心 OLE DB 接口。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 接口  
 若要通过 OLE DB 支持 Udt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 实现了许多的更改，包括添加**ISSCommandWithParameters**接口。 此新接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了三个方法继承自**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，并**SetParameterInfo**;**ISSCommandWithParameters**提供**GetParameterProperties**并**SetParameterProperties**用于处理特定于服务器的方法数据类型。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**接口，还可使用新的 SSPARAMPROPS 结构。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 接口  
 除了**ISSCommandWithParameters**接口，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端还将新值添加到从调用返回的行集**icolumnsrowset:: Getcolumnrowset**方法其中包括。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 目录名称标识符。|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 架构名称标识符。|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|UDT 名称标识符。|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|程序集限定名，其中包括 CLR 引用所需的类型名称和所有程序集标识。|  
  
 通过查看上面指定的添加的 UDT 元数据，可以在 DBCOLUMN_TYPE 设置为 DBTYPE_UDT 时将服务器 UDT 列与其他二进制类型区分开。 如果该数据不完整，服务器类型为 UDT。 对于非 UDT 服务器类型，这些列的返回结果始终为 NULL。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驱动程序  
 在中进行了大量更改[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序支持 Udt。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序映射[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]UDT 到 SQL_SS_UDT 特定于驱动程序的 SQL 数据类型标识符。 UDT 列呈现为 SQL_SS_UDT。 如果您的 UDT 列显式使用映射到 SQL 语句中的另一种类型**ToString**或**ToXMLString**方法的用户定义的类型或通过**CAST/CONVERT**函数中，键入结果中的列集反映了实际类型的列已转换为  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute、SQLDescribeParam、SQLGetDescField  
 添加了四个新的驱动程序特定的描述符字段来提供附加信息的结果集，UDT 列或 UDT 参数的存储过程/参数化查询，以通过检索[SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)， [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)，并[SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)函数。  
  
 这四个新添加的描述符字段分别为 SQL_CA_SS_UDT_CATALOG_NAME、SQL_CA_SS_UDT_SCHEMA_NAME、SQL_CA_SS_UDT_TYPE_NAME 和 SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME。  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns、SQLProcedureColumns  
 此外，将三个新的驱动程序特定列添加到从返回的结果集[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)并[SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md)功能，并提供有关其他信息 UDT 结果设置列或 UDT 参数。 这三个新列分别为 SS_UDT_CATALOG_NAME、SS_UDT_SCHEMA_NAME 和 SS_UDT_ASSEMBLY_TYPE_NAME。  
  
### <a name="supported-conversions"></a>支持的转换  
 从 SQL 转换为 C 数据类型时，SQL_C_WCHAR、SQL_C_BINARY 和 SQL_C_CHAR 可全部转换为 SQL_SS_UDT。 不过请注意，从 SQL_C_WCHAR 和 SQL_C_CHAR SQL 数据类型转换时，二进制数据将转换为十六进制字符串。  
  
 从 C 转换为 SQL 数据类型时，SQL_C_WCHAR、SQL_C_BINARY 和 SQL_C_CHAR 可全部转换为 SQL_SS_UDT。 但是请注意，二进制数据转换为十六进制字符串中，从 SQL_C_WCHAR 和 SQL_C_CHAR SQL 数据类型转换时。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
