---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 713169c273466260872ba29d65ab9c691dc5baf6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  返回 SSPARAMPROPS 属性集结构的数组，每个 UDT 或 XML 参数对应一个 SSPARAMPROPS 属性集。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>参数  
 *pcParams*[out] [in]  
 在中返回指向包含的 SSPARAMPROPS 结构的数目的内存的指针*prgParamProperties*。  
  
 *prgParamProperties*[out 一个]  
 指向内存中将返回 SSPARAMPROPS 结构数组的位置的指针。 提供程序为结构分配内存和的地址返回到此内存;使用者释放此内存， **IMalloc::Free**当不再需要两个结构。 之前调用**IMalloc::Free**为*prgParamProperties*，使用者还必须调用**VariantClear**为*vValue*属性的每个需要的 DBPROP 结构为了防止内存泄漏情况下，该变量包含引用类型 （如 BSTR。)如果*pcParams*是零上的输出或发生 DB_E_ERRORSOCCURRED 其他错误，该提供程序不会分配任何内存，并确保*prgParamProperties*是输出的 null 指针。  
  
## <a name="return-code-values"></a>返回代码值  
 **GetParameterProperties**方法返回作为核心 OLE DB 相同的错误代码**ICommandProperties::GetProperties**不提升方法，但该 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED 除外。  
  
## <a name="remarks"></a>備註  
 **ISSCommandWithParameters::GetParameterProperties**行为保持一致相对于**GetParameterInfo**。 如果[ISSCommandWithParameters::SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)或**SetParameterInfo**尚未调用或与 cParams 等于零，调用了**GetParameterInfo**派生参数信息，并返回此。 如果**ISSCommandWithParameters::SetParameterProperties**或**SetParameterInfo**已调用至少一个参数， **ISSCommandWithParameters::GetParameterProperties**为其返回仅为这些参数的属性**ISSCommandWithParameters::SetParameterProperties**已调用。 如果**ISSCommandWithParameters::SetParameterProperties**后，会调用**ISSCommandWithParameters::GetParameterProperties**或**GetParameterInfo**，因为在后续调用**ISSCommandWithParameters::GetParameterProperties**为其返回的这些参数的重写的值**ISSCommandWithParameters::SetParameterProperties**已调用。  
  
 SSPARAMPROPS 结构的定义如下所示：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|成员|Description|  
|------------|-----------------|  
|*iOrdinal*|所传递参数的序号。|  
|*cPropertySets*|DBPROPSET 数结构中*rgPropertySets*。|  
|*rgPropertySets*|指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
  
## <a name="see-also"></a>另请参阅  
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
