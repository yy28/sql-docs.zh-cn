---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26c95c64f0f2922ef11946841b160879f001e358
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290067"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  返回 SSPARAMPROPS 属性集结构的数组，每个 UDT 或 XML 参数对应一个 SSPARAMPROPS 属性集。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>参数  
 pcParams[out][in]**  
 一个指向内存的指针，该内存包含 prgParamProperties 中返回的 SSPARAMPROPS 结构数量**。  
  
 prgParamProperties[out]**  
 指向内存中将返回 SSPARAMPROPS 结构数组的位置的指针。 提供程序为结构分配内存，并将地址返回到此内存;使用者使用**IMalloc 释放此内存：：** 当它不再需要结构时，它是免费的。 在调用**IMalloc：：对** *prgParamProperties*免费之前，使用者还必须为每个 DBPROP 结构的*vValue*属性调用**VariantClear，** 以防止在变体包含引用类型（如 BSTR）的情况下出现内存泄漏。如果*pcParams*在输出时为零或发生DB_E_ERRORSOCCURRED以外的错误，则提供程序不会分配任何内存，并确保*prgParamProperties*是输出上的空指针。  
  
## <a name="return-code-values"></a>返回代码值  
 **Get参数属性**方法返回与核心 OLE DB **ICommand属性相同的错误代码：：getProperties**方法，但无法引发DB_S_ERRORSOCCURRED和DB_E_ERRORSOCCURED。  
  
## <a name="remarks"></a>备注  
 **ISS命令与参数：：获取参数属性**在**Get参数信息**方面的行为一致。 如果[ISSCommand 与参数：：设置参数属性](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)或**Set 参数信息**尚未调用或已调用 cParams 等于零 **，Getparameterinfo**将派生参数信息并返回此信息。 如果**ISSCommand 与参数：：设置参数属性**或**设置参数信息**已至少调用一个参数，**则 ISSCommand 与参数：get 参数属性**仅返回已为其调用**ISSCommand 与参数：：set 参数属性**的参数的属性。 如果**ISSCommand 与参数：：set 参数属性**在**ISSCommand 与参数：：获取参数属性**或**Getparameterinfo**之后调用，则随后对**ISSCommand 与参数的调用：get 参数属性**返回已调用**ISSCommand 与参数：：set 参数属性**的参数的重写值。  
  
 SSPARAMPROPS 结构的定义如下所示：  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|成员|描述|  
|------------|-----------------|  
|iOrdinal**|所传递参数的序号。|  
|cPropertySets**|rgPropertySets 中 DBPROPSET 结构的数量**。|  
|rgPropertySets**|指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
|||

## <a name="see-also"></a>另请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
