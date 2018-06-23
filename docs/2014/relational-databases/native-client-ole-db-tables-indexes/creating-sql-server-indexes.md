---
title: 创建 SQL Server 索引 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fa0d11ced42d58b7c1b75c2aef7755cbf64b7b69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016597"
---
# <a name="creating-sql-server-indexes"></a>创建 SQL Server 索引
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开**IIndexDefinition::CreateIndex**函数，允许使用者定义新索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序创建表的索引作为索引或约束。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向表所有者、数据库所有者和某些管理角色的成员提供约束创建特权。 默认情况下，只有表所有者才能对表创建索引。 因此，成功还是失败**CreateIndex**不仅取决于应用程序用户的访问权限，但也在创建索引的类型。  
  
 使用者中 Unicode 字符串形式指定表名称*pwszName*的成员*uName*联合中*pTableID*参数。 *EKind*的成员*pTableID*必须 DBKIND_NAME。  
  
 *PIndexID*参数可以为 NULL，而如果是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序创建索引的唯一名称。 使用者可以通过指定指向中 DBID 的有效指针来捕获的索引名称*ppIndexID*参数。  
  
 使用者可以为 Unicode 字符字符串中指定的索引名称*pwszName*的成员*uName*联合的*pIndexID*参数。 *EKind*的成员*pIndexID*必须 DBKIND_NAME。  
  
 使用者按名称指定参与索引的一个或多个列。 为每个 DBINDEXCOLUMNDESC 结构中使用**CreateIndex**、 *eKind*的成员*pColumnID*必须 DBKIND_NAME。 列的名称指定为中的 Unicode 字符字符串*pwszName*的成员*uName*联合中*pColumnID*。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]升序索引中的值的支持。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回 E_INVALIDARG，如果使用者指定 DBINDEX_COL_ORDER_DESC 任何 DBINDEXCOLUMNDESC 结构中。  
  
 **CreateIndex**解释索引属性，如下所示。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试将属性设置**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构中的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_CLUSTERED|读/写： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：控制索引聚类分析。<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序尝试对创建聚集的索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持对任何表最多创建一个聚集索引。<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序尝试上创建非聚集索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。|  
|DBPROP_INDEX_FILLFACTOR|读/写： 读/写<br /><br /> 默认值： 0<br /><br /> 说明：指定用于存储的索引页所占的百分比。 有关详细信息，请参阅[CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql)。<br /><br /> 变量类型为 VT_I4。 该值必须大于或等于 1 且小于或等于 100。|  
|DBPROP_INDEX_INITIALIZE|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试将属性设置**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构中的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_NULLCOLLATION|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试将属性设置**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构中的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_NULLS|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试将属性设置**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构中的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_PRIMARYKEY|读/写： 读/写<br /><br /> 默认值：VARIANT_FALSE 说明：将该索引创建为引用完整性 PRIMARY KEY 约束。<br /><br /> VARIANT_TRUE：创建该索引是为了支持表的 PRIMARY KEY 约束。 列必须不可为 Null。<br /><br /> VARIANT_FALSE：该索引不作为表中行值的 PRIMARY KEY 约束使用。|  
|DBPROP_INDEX_SORTBOOKMARKS|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试将属性设置**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构中的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_TEMPINDEX|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试将属性设置**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构中的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_TYPE|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持此属性。 尝试将属性设置**CreateIndex**导致 DB_S_ERRORSOCCURRED 返回值。 *DwStatus*属性结构中的成员指示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_UNIQUE|读/写： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：对参与的一个或多个列将该索引创建为 UNIQUE 约束。<br /><br /> VARIANT_TRUE：该索引用于唯一约束表中的行值。<br /><br /> VARIANT_FALSE：该索引不对行值进行唯一约束。|  
  
 在提供程序特定属性将设置 DBPROPSET_SQLSERVERINDEX， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序定义的以下数据源信息属性。  
  
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
  
  
