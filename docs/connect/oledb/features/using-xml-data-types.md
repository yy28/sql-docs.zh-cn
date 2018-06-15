---
title: 使用 XML 数据类型 |Microsoft 文档
description: 将 XML 数据类型用于 OLE DB 驱动程序适用于 SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [OLE DB Driver for SQL Server], xml data type
- OLE DB Driver for SQL Server schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- MSOLEDBSQL, XML
- xml data type [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- OLE DB Driver for SQL Server OLE DB interfaces
- XML [SQL Server], OLE DB Driver for SQL Server
- COLUMNS rowset
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d6ec0009a986e2abd56ac00c1e01826f3ed001f7
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612172"
---
# <a name="using-xml-data-types"></a>使用 XML 数据类型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入**xml**使用户可以存储 XML 文档和片段中的数据类型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。 **Xml**数据类型是中的内置数据类型[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，并在某些方面类似于其他内置类型，如是**int**和**varchar**。 因为与其他内置类型，你可以使用**xml**数据类型用作列类型创建表时; 作为变量类型、 参数类型或函数返回类型; 或 CAST 和 CONVERT 函数中。  
  
## <a name="programming-considerations"></a>编程时的注意事项  
 XML 可以是自描述的，即可以根据需要包含一个 XML 标头来指定文档的编码，例如：  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 XML 标准描述 XML 处理器如何通过检查文档的前若干个字节来检测用于文档的编码。 有时，应用程序指定的编码可能与文档指定的编码相冲突。 对于作为绑定参数传递的文档，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将 XML 视为二进制数据，因此不执行转换，并且 XML 分析器可以使用在文档内指定的编码而不会出现问题。 然而，对于绑定为 WSTR 的 XML 数据，应用程序必须确保将文档编码为 Unicode。 这种情况下可能需要加载到 DOM 中的文档、 更改编码为 Unicode，和序列化文档中。 如果未完成此步骤，则数据转换可能会发生，从而导致无效或已损坏的 XML。  
  
 当在文字中指定 XML 时，也可能发生冲突。 例如，下面的内容无效：  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序 
 DBTYPE_XML 是特定于 SQL Server 的 OLE DB 驱动程序中的 XML 的新数据类型。 此外，可以通过现有的 OLE DB 类型（DBTYPE_BYTES、DBTYPE_WSTR、DBTYPE_BSTR、DBTYPE_XML、DBTYPE_STR、DBTYPE_VARIANT 和 DBTYPE_IUNKNOWN）访问 XML 数据。 可以采用以下格式的 SQL Server 行集 OLE DB 驱动程序中的列中检索的 XML 类型列中存储的数据：  
  
-   文本字符串  
  
-   **ISequentialStream**  
  
> [!NOTE]  
>  SQL Server 的 OLE DB 驱动程序不包括 SAX 读取器，但**ISequentialStream**可以轻松地传递给在 MSXML 中的 SAX 和 DOM 对象。  
  
 **ISequentialStream**应该用于检索大型 XML 文档。 用于其他大值类型的相同技术也适用于 XML。 有关详细信息，请参阅[使用大值类型](../../oledb/features/using-large-value-types.md)。  
  
 此外可以检索在行集中的 XML，类型的列中存储的数据插入或更新应用程序通过常用接口如**IRow::GetColumns**， **IRowChange::SetColumns**，和**ICommand::Execute**。 同样到检索的情况下，应用程序可以传递文本字符串或**ISequentialStream**到 SQL Server 的 OLE DB 驱动程序。  
  
> [!NOTE]  
>  将 XML 数据发送到的字符串格式**ISequentialStream**接口，你必须获取**ISequentialStream**通过指定 DBTYPE_IUNKNOWN 并设置其*pObject*为 null 的绑定中的自变量。  
  
 当由于使用者缓冲区过小而导致已检索的 XML 数据被截断时，长度可能作为 0xffffffff 返回，这意味着长度为未知的。 此行为是作为数据类型，而无需发送之前的实际数据长度信息流式传输到客户端符合其实现。 提供了缓冲整个值，如时，则可能返回在某些情况下，实际长度**irowset:: Getdata**并执行数据转换。  
  
 服务器会将发送到 SQL Server 的 XML 数据视为二进制数据。 此行为可防止发生任何转换，并允许自动检测的 XML 编码 XML 分析器。 这样，就可以接受更广泛的 XML 文档（例如，以 UTF-8 编码的文档）作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的输入。  
  
 如果将输入 XML 绑定为 DBTYPE_WSTR，则应用程序必须确保已对其进行 Unicode 编码，以避免由于不必要的数据转换而可能导致损坏。  
  
### <a name="data-bindings-and-coercions"></a>数据绑定和强制  
 下表介绍的绑定和使用列出的数据类型与时发生的强制[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **xml**数据类型。  
  
|数据类型|到服务器<br /><br /> **XML**|到服务器<br /><br /> **非 XML**|从服务器<br /><br /> **XML**|从服务器<br /><br /> **非 XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|将通过<sup>6，7</sup>|错误<sup>1</sup>|确定<sup>11、 6</sup>|错误<sup>8</sup>|  
|DBTYPE_BYTES|将通过<sup>6，7</sup>|N/A<sup>2</sup>|确定<sup>11、 6</sup>|N/A <sup>2</sup>|  
|DBTYPE_WSTR|将通过<sup>6,10</sup>|N/A <sup>2</sup>|确定<sup>4、 6、 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_BSTR|将通过<sup>6,10</sup>|N/A <sup>2</sup>|确定<sup>3</sup>|N/A <sup>2</sup>|  
|DBTYPE_STR|确定<sup>6、 9、 10</sup>|N/A <sup>2</sup>|确定<sup>5、 6、 12</sup>|N/A <sup>2</sup>|  
|DBTYPE_IUNKNOWN|字节流通过**ISequentialStream**<sup>7</sup>|N/A <sup>2</sup>|字节流通过**ISequentialStream**<sup>11</sup>|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &AMP;#124; VT_ARRAY)|将通过<sup>6，7</sup>|N/A <sup>2</sup>|N/A|N/A <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|将通过<sup>6,10</sup>|N/A <sup>2</sup>|确定<sup>3</sup>|N/A <sup>2</sup>|  
  
 <sup>1</sup>如果服务器的类型是其他不是使用指定 DBTYPE_XML **ICommandWithParameters::SetParameterInfo**和访问器类型是 DBTYPE_XML，执行语句时出错 (DB_E_ERRORSOCCURRED，参数状态为 DBSTATUS_E_BADACCESSOR）;否则将数据发送到服务器，但服务器将返回一个错误，指示从 XML 没有隐式转换为参数的数据类型。  
  
 <sup>2</sup>超出本文的范围。  
  
 <sup>3</sup>格式为 utf-16，没有 bye 顺序标记 (BOM) 没有编码的规范，任何 null 终止。  
  
 <sup>4</sup>格式为 utf-16，没有 BOM，没有编码规范，null 终止。  
  
 <sup>5</sup>格式是在与 null 终止符的客户端代码页编码的多字节字符。 从服务器转换提供的 Unicode 可能会导致数据损坏，因此不建议使用此绑定。  
  
 <sup>6</sup>BY_REF 可能会使用。  
  
 <sup>7</sup>utf-16 数据必须以 BOM 开头。 否则，服务器可能无法正确地识别编码。  
  
 <sup>8</sup>验证可能发生在创建访问器时，或在提取时间。 此错误为 DB_E_ERRORSOCCURRED，绑定状态设置为 DBBINDSTATUS_UNSUPPORTEDCONVERSION。  
  
 <sup>9</sup>数据转换为 Unicode 在发送到服务器之前使用的客户端代码页。 如果文档编码与客户端代码页不匹配，则可能会导致数据损坏，因此此绑定是强烈建议不要使用。  
  
 <sup>10</sup>BOM 始终将添加到数据发送到服务器。 如果数据已经开始包含 BOM，将有两个物料清单的缓冲区的开头。 服务器使用第一个 BOM 来识别为 utf-16 编码，然后放弃它。 第二个 BOM 将被解释为零宽度不间断空格字符。  
  
 <sup>11</sup>格式为 utf-16，没有编码的规范，BOM 将添加到从服务器收到的数据。 如果服务器返回空字符串，BOM 仍会返回到应用程序。 如果缓冲区长度奇数个字节，数据将被正确截断。 如果整个值返回成多个块，它们可以串联来重建正确的值。  
  
 <sup>12</sup>缓冲区长度是否少于两个字符-即，没有足够的空间 null 终止-报告溢出错误。  
  
> [!NOTE]  
>  对于 NULL XML 值，不返回值。  
  
 XML 标准要求 UTF-16 编码的 XML，以便以字节顺序标记 (BOM) UTF-16 字符代码 0xFEFF 开头。 在使用 WSTR 和 BSTR 绑定，OLE DB 驱动程序的 SQL Server 并不要求或添加 BOM，如的编码会进行隐式绑定。 当使用 BYTES、XML 或 IUNKNOWN 绑定时，目的是为了在处理其他 XML 处理器和存储系统时提供简便性。 在这种情况下，BOM 应该会存在与 UTF 16 编码的 XML，和应用程序需要不会关心的实际编码，因为 XML 处理器 （包括 SQL Server） 的大部分推导通过检查值的前几个字节的编码。 XML 数据从 OLE DB 驱动程序收到使用字节，XML，为 SQL Server 或 IUNKNOWN 绑定始终编码的 utf-16 BOM 使用和不使用嵌入的编码声明。  
  
 OLE DB 核心服务提供的数据转换 (**IDataConvert**) 不适用于 DBTYPE_XML。  
  
 当向服务器发送数据时将执行验证。 应通过你的应用程序处理客户端验证和编码更改。 建议你不直接处理 XML 数据，但应改用 DOM 或 SAX 读取器来对其进行处理。  
  
 可以绑定 DBTYPE_NULL 和 DBTYPE_EMPTY，用于输入参数，但不是能为输出参数或结果。 当将它们绑定用于输入参数时，状态必须设置为 DBSTATUS_S_ISNULL 或 DBSTATUS_S_DEFAULT。  
  
 可以将 DBTYPE_XML 转换为 DBTYPE_EMPTY 和 DBTYPE_NULL，并可以将 DBTYPE_EMPTY 转换为 DBTYPE_XML，但无法将 DBTYPE_NULL 转换为 DBTYPE_XML。 这与 DBTYPE_WSTR 相一致。  
  
 DBTYPE_IUNKNOWN 是支持的绑定 （如前面的表所示），但没有 DBTYPE_XML 和 DBTYPE_IUNKNOWN 之间转换。 DBTYPE_IUNKNOWN 不能与 DBTYPE_BYREF 一起使用。  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 行集的添加和更改内容  
 OLE DB 驱动程序的 SQL Server 添加新值，或更改到多个核心 OLE DB 架构行集。  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>COLUMNS 和 PROCEDURE_PARAMETERS 架构行集  
 添加列和 PROCEDURE_PARAMETERS 架构行集包括以下各列：  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|在其中定义 XML 架构集合的目录的名称。 为非 XML 列或非类型化的 XML 列的为 NULL。|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|在其中定义 XML 架构集合的架构的名称。 为非 XML 列或非类型化的 XML 列的为 NULL。|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 架构集合的名称。 为非 XML 列或非类型化的 XML 列的为 NULL。|  
  
#### <a name="the-providertypes-schema-rowset"></a>PROVIDER_TYPES 架构行集  
 PROVIDER_TYPES 架构行集，在 COLUMN_SIZE 值是 0 **xml**数据类型，并且 DATA_TYPE DBTYPE_XML。  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>SS_XMLSCHEMA 架构行集  
 所引入的新的架构行集 SS_XMLSCHEMA 可供客户端检索 XML 架构信息。 SS_XMLSCHEMA 行集包含以下列：  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 集合所属的目录。|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 集合所属的架构。|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 架构集合的类型化的 XML 列，为 NULL 则名称。|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|XML 架构的目标命名空间。|  
|SCHEMACONTENT|DBTYPE_WSTR|XML 架构内容。|  
  
 每个 XML 架构都按目录名称、架构名称、架构集合名称和目标命名空间统一资源标识符 (URI) 限定范围。 此外，还定义了新的 GUID，其名称为 DBSCHEMA_XML_COLLECTIONS。 SS_XMLSCHEMA 架构行集的限制数和受限列定义如下。  
  
|GUID|限制数|受限列|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB 属性集的添加和更改内容  
 OLE DB 驱动程序的 SQL Server 添加新值，或更改到多个核心 OLE DB 属性集。  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 属性集  
 为了支持**xml**数据类型通过 OLE DB，OLE DB 驱动程序的 SQL Server 实现新的 DBPROPSET_SQLSERVERPARAMETER 属性集，其中包含以下值。  
  
|“属性”|类型|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|在其中定义 XML 架构集合的目录（数据库）的名称。 SQL 三部分组成的名称标识符的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|架构集合内 XML 架构的名称。 由三部分组成的 SQL 名称标识符的一部分。|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|目录内 XML 架构集合的名称。由三部分组成的 SQL 名称标识符的一部分。|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 属性集  
 若要支持中的表创建**ITableDefinition**接口，OLE DB 驱动程序的 SQL Server 将三个新列添加到 DBPROPSET_SQLSERVERCOLUMN 属性集。  
  
|“属性”|类型|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|对于类型化 XML 列，此属性是一个字符串，它指定在其中存储 XML 架构的目录的名称。 对于其他列类型，此属性返回一个空字符串。|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|对于类型化 XML 列，此属性是一个字符串，它指定定义此列的 XML 架构的名称。|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|对于类型化 XML 列，此属性是一个字符串，它指定定义此值的 XML 架构集合的名称。|  
  
 与 SSPROP_PARAM 值类似，所有这些属性都是可选的且默认值为空。 仅当指定 SSPROP_COL_XML_SCHEMACOLLECTIONNAME 时，才能指定 SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME 和 SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME。 在将 XML 传递到服务器时，如果包含这些值，则将针对当前数据库检查它们是否存在（有效性），并且针对架构检查实例数据。 在所有情况下，要使这些值有效，它们必须全部为空或全部添入这些值。  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 接口的添加和更改内容  
 OLE DB 驱动程序的 SQL Server 添加新值，或到多个 OLE DB 接口的核心更改。  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 接口  
 为了支持**xml**数据类型通过 OLE DB，OLE DB 驱动程序的 SQL Server 实现大量的更改包括添加[ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)接口。 此新接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了从继承的三个方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供[GetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)和[SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)用于处理服务器特定的方法数据类型。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**接口还可以使用新 SSPARAMPROPS 的结构。  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 接口  
 OLE DB 驱动程序的 SQL Server 将添加以下[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-到返回的行集的特定列**IColumnRowset::GetColumnsRowset**方法。 这些列包含 XML 架构集合的由三个部分组成的名称。 对于非 XML 列或非类型化 XML 列，所有这三列均取默认值 NULL。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 架构集合所属的目录，<br /><br /> 否则为 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 架构集合所属的架构。 否则为 NULL。|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|类型化 XML 列的 XML 架构集合的名称，否则为 NULL。|  
  
#### <a name="the-irowset-interface"></a>IRowset 接口  
 XML 列中的 XML 实例检索通过**irowset:: Getdata**方法。 根据由客户端指定的绑定，可以将 XML 实例作为 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML、DBTYPE_STR、DBTYPE_BYTES 进行检索，或者通过 DBTYPE_IUNKNOWN 将其作为接口检索。 如果使用者指定 DBTYPE_BSTR、DBTYPE_WSTR 或 DBTYPE_VARIANT，则访问接口将 XML 实例转换为用户请求的类型，并将其放入在相应绑定中指定的位置。  
  
 如果使用者指定 DBTYPE_IUNKNOWN 和设置*pObject*自变量为 NULL，或者设置*pObject* IID_ISequentialStream 自变量，该提供程序返回**ISequentialStream**接口向使用者，以便使用者可以流式传输超出列的 XML 数据。 **ISequentialStream**然后返回为 Unicode 字符流的 XML 数据。  
  
 当返回与 DBTYPE_IUNKNOWN 绑定的 XML 值时，访问接口将报告 `sizeof (IUnknown *)` 的大小值。 此行为是与某一列绑定为 DBTYPE_IUnknown 或 DBTYPE_IDISPATCH，和由 DBTYPE_IUNKNOWN/ISequentialStream 时无法确定确切的列大小时采取的方法一致。  
  
#### <a name="the-irowsetchange-interface"></a>IRowsetChange 接口  
 使用者可以通过两种方法更新列中的 XML 实例。 第一个参数是通过存储对象**ISequentialStream**创建提供程序。 使用者可以调用**ISequentialStream::Write**方法来直接更新提供程序返回的 XML 实例。  
  
 第二种方法是通过**IRowsetChange::SetData**或**IRowsetChange::InsertRow**方法。 通过这一方法，可以在类型为 DBTYPE_BSTR、DBTYPE_WSTR、DBTYPE_VARIANT、DBTYPE_XML 或 DBTYPE_IUNKNOWN 的绑定中指定使用者缓冲区内的 XML 实例。  
  
 如果指定 DBTYPE_BSTR、 DBTYPE_WSTR 或 DBTYPE_VARIANT，则提供程序将存储到正确的列驻留在使用者缓冲区中的 XML 实例。  
  
 如果指定 DBTYPE_IUNKNOWN/ISequentialStream，如果使用者未指定任何存储对象时，必须创建使用者**ISequentialStream**提前对象，将绑定对象的 XML 文档，然后将传递对象提供程序通过**IRowsetChange::SetData**方法。 使用者还可以创建一个存储对象，将 pObject 参数设置为 IID_ISequentialStream，创建**ISequentialStream**对象，然后将传递**ISequentialStream**对象传递给**IRowsetChange::SetData**方法。 在这两种情况下，提供程序可以检索 XML 对象，通过**ISequentialStream**对象，并将其插入到正确的列。  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate 接口  
 **IRowsetUpdate**接口提供了用于延迟的更新功能。 提供给行集的数据也不会提供其他事务之前使用者调用**IRowsetUpdate::Update**方法。  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind 接口  
 **IRowsetFind::FindNextRow**方法并不适用于**xml**数据类型。 当**IRowsetFind::FindNextRow**称为和*hAccessor*自变量指定 DBTYPE_XML 一列，返回 DB_E_BADBINDINFO。 此时不考虑正在搜索的列的类型。 对于任何其他绑定类型， **FindNextRow**如果要在其中搜索此列属于失败并 DB_E_BADCOMPAREOP **xml**数据类型。  
 
  
## <a name="see-also"></a>请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
