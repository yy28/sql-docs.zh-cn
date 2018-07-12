---
title: 创建 SQL Server 索引 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 21d6af3f02baa2e5c3a0a70cc1bf48119b14f60e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424956"
---
# <a name="creating-sql-server-indexes"></a>创建 SQL Server 索引
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开**iindexdefinition:: Createindex**函数，从而允许使用者定义的新索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序创建表索引作为索引或约束。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向表所有者、数据库所有者和某些管理角色的成员提供约束创建特权。 默认情况下，只有表所有者才能对表创建索引。 因此，成功还是失败**CreateIndex**不仅取决于应用程序用户的访问权限，而且还在创建索引的类型。  
  
 使用者指定为 Unicode 字符串中的表名*pwszName*的成员*uName*联合*pTableID*参数。 *EKind*的成员*pTableID*必须为 DBKIND_NAME。  
  
 *PIndexID*参数可以为 NULL，而如果是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口创建索引的唯一名称。 使用者可以捕获索引的名称，通过指定指向中 DBID 的有效指针*ppIndexID*参数。  
  
 使用者可以为 Unicode 字符字符串中指定索引名称*pwszName*的成员*uName*的联合*pIndexID*参数。 *EKind*的成员*pIndexID*必须为 DBKIND_NAME。  
  
 使用者按名称指定参与索引的一个或多个列。 为每个 DBINDEXCOLUMNDESC 结构中使用**CreateIndex**，则*eKind*的成员*pColumnID*必须为 DBKIND_NAME。 为 Unicode 字符字符串中指定的列的名称*pwszName*的成员*uName*联合*pColumnID*。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]升序索引中的值的支持。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果使用者在任何 DBINDEXCOLUMNDESC 结构中指定 DBINDEX_COL_ORDER_DESC，Native Client OLE DB 访问接口将返回 E_INVALIDARG。  
  
 **CreateIndex**索引属性的解释，如下所示。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/w： 读/写<br /><br /> 默认值： 无<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试设置中的属性**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_CLUSTERED|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：控制索引聚类分析。<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口尝试创建聚集的索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持对任何表最多创建一个聚集索引。<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口尝试对创建非聚集索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。|  
|DBPROP_INDEX_FILLFACTOR|R/w： 读/写<br /><br /> 默认值： 0<br /><br /> 说明：指定用于存储的索引页所占的百分比。 有关详细信息，请参阅[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)。<br /><br /> 变量类型为 VT_I4。 该值必须大于或等于 1 且小于或等于 100。|  
|DBPROP_INDEX_INITIALIZE|R/w： 读/写<br /><br /> 默认值： 无<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试设置中的属性**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_NULLCOLLATION|R/w： 读/写<br /><br /> 默认值： 无<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试设置中的属性**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_NULLS|R/w： 读/写<br /><br /> 默认值： 无<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试设置中的属性**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_PRIMARYKEY|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE 说明：将该索引创建为引用完整性 PRIMARY KEY 约束。<br /><br /> VARIANT_TRUE：创建该索引是为了支持表的 PRIMARY KEY 约束。 列必须不可为 Null。<br /><br /> VARIANT_FALSE：该索引不作为表中行值的 PRIMARY KEY 约束使用。|  
|DBPROP_INDEX_SORTBOOKMARKS|R/w： 读/写<br /><br /> 默认值： 无<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试设置中的属性**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_TEMPINDEX|R/w： 读/写<br /><br /> 默认值： 无<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试设置中的属性**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_TYPE|R/w： 读/写<br /><br /> 默认值： 无<br /><br /> 说明： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试设置中的属性**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_UNIQUE|R/w： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：对参与的一个或多个列将该索引创建为 UNIQUE 约束。<br /><br /> VARIANT_TRUE：该索引用于唯一约束表中的行值。<br /><br /> VARIANT_FALSE：该索引不对行值进行唯一约束。|  
  
 在特定于提供程序的属性集 DBPROPSET_SQLSERVERINDEX 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口定义以下数据源信息属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|类型：VT_BOOL (R/W)<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：当使用 IIndexDefinition::CreateIndex 将此属性指定为值 VARIANT_TRUE 时，将导致创建与被索引的列对应的主 xml 索引。 如果此属性为 VARIANT_TRUE，则 cIndexColumnDescs 应为 1，否则将会出错。|  
  
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
  
  
