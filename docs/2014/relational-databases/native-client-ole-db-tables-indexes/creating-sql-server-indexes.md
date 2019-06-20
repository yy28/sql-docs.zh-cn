---
title: 创建 SQL Server 索引 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bda39528b6bc04fbff6faa4c72d85a4eccd576c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046449"
---
# <a name="creating-sql-server-indexes"></a>创建 SQL Server 索引
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开**iindexdefinition:: Createindex**函数，从而允许使用者定义的新索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序创建表索引作为索引或约束。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向表所有者、数据库所有者和某些管理角色的成员提供约束创建特权。 默认情况下，只有表所有者才能对表创建索引。 因此，CreateIndex 的成功或失败不仅取决于应用程序用户的访问权限，还取决于所创建索引的类型  。  
  
 在 pTableID 参数的 uName 联合的 pwszName 成员中，使用者将表名指定为 Unicode 字符串    。 pTableID 的 eKind 成员必须是 DBKIND_NAME   。  
  
 *PIndexID*参数可以为 NULL，而如果是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口创建索引的唯一名称。 通过在 ppIndexID 参数中指定一个指向 DBID 的有效指针，使用者可以捕获索引的名称  。  
  
 在 pIndexID 参数的 uName 联合的 pwszName 成员中，使用者可以将索引名称指定为 Unicode 字符串    。 pIndexID 的 eKind 成员必须是 DBKIND_NAME   。  
  
 使用者按名称指定参与索引的一个或多个列。 对于在 CreateIndex 中使用的每个 DBINDEXCOLUMNDESC 结构，pColumnID 的 eKind 成员必须为 DBKIND_NAME    。 在 pColumnID 的 uName 联合的 pwszName 成员中，列名指定为 Unicode 字符串    。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]升序索引中的值的支持。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果使用者在任何 DBINDEXCOLUMNDESC 结构中指定 DBINDEX_COL_ORDER_DESC，Native Client OLE DB 访问接口将返回 E_INVALIDARG。  
  
 CreateIndex 对索引属性的解释如下  。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/W:读/写<br /><br /> 默认值：None<br /><br /> 说明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试在 CreateIndex 中设置此属性将导致出现 DB_S_ERRORSOCCURRED 返回值  。 此属性结构的 dwStatus 成员指示 DBPROPSTATUS_BADVALUE  。|  
|DBPROP_INDEX_CLUSTERED|R/W:读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明:控制索引聚类分析。<br /><br /> VARIANT_TRUE:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口尝试创建聚集的索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持对任何表最多创建一个聚集索引。<br /><br /> VARIANT_FALSE:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口尝试对创建非聚集索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。|  
|DBPROP_INDEX_FILLFACTOR|R/W:读/写<br /><br /> 默认值：0<br /><br /> 说明:指定用于存储索引页的百分比。 有关详细信息，请参阅[创建索引](/sql/t-sql/statements/create-index-transact-sql)。<br /><br /> 变量类型为 VT_I4。 该值必须大于或等于 1 且小于或等于 100。|  
|DBPROP_INDEX_INITIALIZE|R/W:读/写<br /><br /> 默认值：None<br /><br /> 说明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试在 CreateIndex 中设置此属性将导致出现 DB_S_ERRORSOCCURRED 返回值  。 此属性结构的 dwStatus 成员指示 DBPROPSTATUS_BADVALUE  。|  
|DBPROP_INDEX_NULLCOLLATION|R/W:读/写<br /><br /> 默认值：None<br /><br /> 说明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试在 CreateIndex 中设置此属性将导致出现 DB_S_ERRORSOCCURRED 返回值  。 此属性结构的 dwStatus 成员指示 DBPROPSTATUS_BADVALUE  。|  
|DBPROP_INDEX_NULLS|R/W:读/写<br /><br /> 默认值：None<br /><br /> 说明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试在 CreateIndex 中设置此属性将导致出现 DB_S_ERRORSOCCURRED 返回值  。 此属性结构的 dwStatus 成员指示 DBPROPSTATUS_BADVALUE  。|  
|DBPROP_INDEX_PRIMARYKEY|R/W:读/写<br /><br /> 默认值：VARIANT_FALSE 说明：该索引创建为引用完整性，PRIMARY KEY 约束。<br /><br /> VARIANT_TRUE:创建索引以支持表的 PRIMARY KEY 约束。 列必须不可为 Null。<br /><br /> VARIANT_FALSE:索引不用作表中的行值的 PRIMARY KEY 约束。|  
|DBPROP_INDEX_SORTBOOKMARKS|R/W:读/写<br /><br /> 默认值：None<br /><br /> 说明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试在 CreateIndex 中设置此属性将导致出现 DB_S_ERRORSOCCURRED 返回值  。 此属性结构的 dwStatus 成员指示 DBPROPSTATUS_BADVALUE  。|  
|DBPROP_INDEX_TEMPINDEX|R/W:读/写<br /><br /> 默认值：None<br /><br /> 说明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试在 CreateIndex 中设置此属性将导致出现 DB_S_ERRORSOCCURRED 返回值  。 此属性结构的 dwStatus 成员指示 DBPROPSTATUS_BADVALUE  。|  
|DBPROP_INDEX_TYPE|R/W:读/写<br /><br /> 默认值：None<br /><br /> 说明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试在 CreateIndex 中设置此属性将导致出现 DB_S_ERRORSOCCURRED 返回值  。 此属性结构的 dwStatus 成员指示 DBPROPSTATUS_BADVALUE  。|  
|DBPROP_INDEX_UNIQUE|R/W:读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明:该索引创建为参与列或列的唯一约束。<br /><br /> VARIANT_TRUE:索引用于唯一约束的表中的行值。<br /><br /> VARIANT_FALSE:索引不唯一约束的行值。|  
  
 在特定于提供程序的属性集 DBPROPSET_SQLSERVERINDEX 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义以下数据源信息属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|键入：VT_BOOL (R/W)<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明:如果值为 VARIANT_TRUE 使用 iindexdefinition:: Createindex 指定此属性，它会导致正在创建要编制索引的列相对应的主 xml 索引。 如果此属性为 VARIANT_TRUE，则 cIndexColumnDescs 应为 1，否则将会出错。|  
  
 本示例创建了一个主键索引：  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>请参阅  
 [表和索引](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
