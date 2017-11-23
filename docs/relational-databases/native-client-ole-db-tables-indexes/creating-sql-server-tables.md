---
title: "创建 SQL Server 表 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0885cda5de0621de5ffbd85a318ab90887bc536
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="creating-sql-server-tables"></a>创建 SQL Server 表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开**ITableDefinition::CreateTable**函数，允许使用者创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 使用者使用**CreateTable**若要创建具有生成的唯一名称的使用者名称永久表和永久或临时表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。  
  
 当使用者调用**ITableDefinition::CreateTable**，如果 DBPROP_TBL_TEMPTABLE 属性的值是 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序生成使用者的临时表名称。 使用者集*pTableID*参数**CreateTable**为 NULL 的方法。 生成名称与临时表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序不显示在**表**行集，但可通过访问**IOpenRowset**接口。  
  
 当使用者指定中的表名称*pwszName*的成员*uName*联合中*pTableID*参数， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有该名称的表。 将应用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表命名约束，并且表名可以指示永久表或者指示本地或全局临时表。 有关详细信息，请参阅[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)。 *PpTableID*参数可以为 NULL。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序可以生成永久或临时表的名称。 当使用者设置*pTableID*参数为 NULL，且集*ppTableID*以指向有效的 DBID\*、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回的表中的生成的名称*pwszName*的成员*uName* DBID 联合指向的值*ppTableID*。 若要创建一个临时的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序名为表中，使用者包含 OLE DB 表属性 DBPROP_TBL_TEMPTABLE 中设置中引用的表属性*rgPropertySets*参数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序名为临时表是本地的。  
  
 **CreateTable**如果返回 DB_E_BADTABLEID *eKind*的成员*pTableID*参数不表示 DBKIND_NAME。  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 使用情况  
 使用者可以通过使用指示的列数据类型*pwszTypeName*成员或*wType*成员。 如果使用者指定中的数据类型*pwszTypeName*、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将忽略的值*wType*。  
  
 如果使用*pwszTypeName*成员，使用者通过使用指定的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型名称。 有效的数据类型名称是在 PROVIDER_TYPES 架构行集的 TYPE_NAME 列中返回的名称。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序识别中的 OLE DB 枚举 DBTYPE 值一部分*wType*成员。 有关详细信息，请参阅[Data Type Mapping 中 ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。  
  
> [!NOTE]  
>  **CreateTable**返回 DB_E_BADTYPE，如果使用者设置*pTypeInfo*或*pclsid*成员来指定列数据类型。  
  
 使用者指定中的列名称*pwszName*的成员*uName*联合的 DBCOLUMNDESC *dbcid*成员。 该列名指定为 Unicode 字符串。 *EKind*的成员*dbcid*必须 DBKIND_NAME。 **CreateTable**如果返回 DB_E_BADCOLUMNID *eKind*是无效的*pwszName*为 NULL，或者如果的值*pwszName*不是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符。  
  
 所有列属性均可用于为表定义的所有列上。 **CreateTable**可以返回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED 如果冲突设置属性值。 **CreateTable**无效的列属性设置而导致发生时将返回错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表创建失败。  
  
 DBCOLUMNDESC 中的列属性解释如下。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|读/写： 读/写<br /><br /> 默认值：VARIANT_FALSE。说明：对于所创建的列设置标识属性。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，标识属性对表中的单一列有效。 有关详细信息比单个列所生成错误将属性设置为 VARIANT_TRUE 时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序尝试在服务器上创建表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识属性才是有效的**整数**，**数值**，和**十进制**类型小数位数为 0 时。 对任何其他数据类型的列将属性设置为 VARIANT_TRUE 生成一个错误时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序尝试在服务器上创建表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回 DB_S_ERRORSOCCURRED DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 均为这两个 VARIANT_TRUE 时与*dwOption* DBPROP_COL_NULLABLE 不 DBPROPOPTIONS_REQUIRED。 当 DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 为这两个 VARIANT_TRUE 返回 DB_E_ERRORSOCCURRED 和*dwOption*的 DBPROP_COL_NULLABLE 等于 DBPROPOPTIONS_REQUIRED。 列定义与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识属性和 DBPROP_COL_NULLABLE *dwStatus*成员设置为 DBPROPSTATUS_CONFLICTING。|  
|DBPROP_COL_DEFAULT|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 说明：为该列创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DEFAULT 约束。<br /><br /> *VValue*需要的 DBPROP 成员可以是任何类型的数字。 *VValue.vt*成员应指定与列的数据类型兼容的类型。 例如，对于定义为 DBTYPE_WSTR 的某列将 BSTR N/A 定义为默认值就是一个兼容的匹配。 在定义为 DBTYPE_R8 生成错误的列上定义了相同的默认值时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序尝试在服务器上创建表。|  
|DBPROP_COL_DESCRIPTION|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： 未实现通过 DBPROP_COL_DESCRIPTION 列属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。<br /><br /> *DwStatus*需要的 DBPROP 结构中的成员返回 DBPROPSTATUS_NOTSUPPORTED 时使用者都尝试写入属性值。<br /><br /> 设置属性，不会导致严重错误以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 如果所有其他参数值有效，则创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。|  
|DBPROP_COL_FIXEDLENGTH|读/写： 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用 DBPROP_COL_FIXEDLENGTH 以确定何时使用者通过使用来定义列的数据类型的数据类型映射*wType* DBCOLUMNDESC 的成员。 有关详细信息，请参阅[Data Type Mapping 中 ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。|  
|DBPROP_COL_NULLABLE|读/写： 读/写<br /><br /> 默认值： 无<br /><br /> 描述： 在创建表， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序指示是否在设置该属性列是否应接受 null 值。 如果未设置此属性，则该列能否接受 NULL 作为值将由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 默认数据库选项确定。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序是符合 ISO 标准的提供程序。 所连接的会话展现 ISO 行为。 如果使用者未设置 DBPROP_COL_NULLABLE，则列接受 NULL 值。|  
|DBPROP_COL_PRIMARYKEY|读/写： 读/写<br /><br /> 默认值： VARIANT_FALSE 说明： 当 VARIANT_TRUE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将列创建 PRIMARY KEY 约束。<br /><br /> 当定义为列属性时，仅单一列能够确定约束。 VARIANT_TRUE 将属性设置的时间超过单个列返回一个错误时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序尝试创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。<br /><br /> 注意： 使用者可以使用**IIndexDefinition::CreateIndex**创建两个或多个列的主键约束。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回 DB_S_ERRORSOCCURRED DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 均为这两个 VARIANT_TRUE 时与*dwOption* DBPROP_COL_UNIQUE 不 DBPROPOPTIONS_REQUIRED。<br /><br /> 当 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 为这两个 VARIANT_TRUE 返回 DB_E_ERRORSOCCURRED 和*dwOption*的 DBPROP_COL_UNIQUE 等于 DBPROPOPTIONS_REQUIRED。 列定义与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识属性和 DBPROP_COL_PRIMARYKEY *dwStatus*成员设置为 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回错误，当 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_NULLABLE 为这两个 VARIANT_TRUE。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回了一个来自错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时使用者都尝试创建 PRIMARY KEY 约束的无效列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。 无法创建与列上定义 PRIMARY KEY 约束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型**位**，**文本**， **ntext**，和**映像**。|  
|DBPROP_COL_UNIQUE|读/写： 读/写<br /><br /> 默认值：VARIANT_FALSE。说明：将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UNIQUE 约束应用于列。<br /><br /> 当定义为列属性时，此约束仅应用于单一列。 使用者可以使用**IIndexDefinition::CreateIndex**将两个或多个列的组合值的唯一约束。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回 DB_S_ERRORSOCCURRED DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 均为这两个 VARIANT_TRUE 时和*dwOption*不 DBPROPOPTIONS_REQUIRED。<br /><br /> 当 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 为这两个 VARIANT_TRUE 返回 DB_E_ERRORSOCCURRED 和*dwOption*等于 DBPROPOPTIONS_REQUIRED。 列定义与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识属性和 DBPROP_COL_PRIMARYKEY *dwStatus*成员设置为 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回 DB_S_ERRORSOCCURRED DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 均为这两个 VARIANT_TRUE 时和*dwOption*不 DBPROPOPTIONS_REQUIRED。<br /><br /> 当 DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 为这两个 VARIANT_TRUE 返回 DB_E_ERRORSOCCURRED 和*dwOption*等于 DBPROPOPTIONS_REQUIRED。 列定义与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识属性和 DBPROP_COL_NULLABLE *dwStatus*成员设置为 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回了一个来自错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时使用者都尝试创建唯一约束的无效列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。 无法创建与列上定义唯一约束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**位**数据类型。|  
  
 当使用者调用**ITableDefinition::CreateTable**、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序，如下所示解释表属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|读/写： 读/写<br /><br /> 默认值： VARIANT_FALSE 说明： 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序创建的使用者名称的表。 当 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序生成使用者的临时表名称。 使用者集*pTableID*参数**CreateTable**为 NULL。 *PpTableID*参数必须包含有效的指针。|  
  
 如果使用者请求已成功创建表，打开行集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序打开游标支持行集。 可以在所传递的属性集中指示任何行集属性。  
  
 此示例创建一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
