---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) |Microsoft Docs'
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5e03e1ef1cd62dda40cd9b138c3d2ff3d7395ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050987"
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
 pcParams[out][in]   
 一个指向内存的指针，该内存包含 prgParamProperties 中返回的 SSPARAMPROPS 结构数量  。  
  
 prgParamProperties[out]   
 指向内存中将返回 SSPARAMPROPS 结构数组的位置的指针。 提供程序为结构分配内存，并返回此内存; 地址使用者释放此内存以及**imalloc:: Free**它不再需要这些结构。 然后再调用**imalloc:: Free**有关*prgParamProperties*，使用者还必须调用**VariantClear**有关*vValue*属性为了防止内存泄漏情况下，该变量包含引用的每个 DBPROP 结构的类型 （例如 BSTR。)如果*pcParams*是零个在输出或发生错误 DB_E_ERRORSOCCURRED 之外，该提供程序不会分配任何内存并且可确保*prgParamProperties*是输出的 null 指针。  
  
## <a name="return-code-values"></a>返回代码值  
 **GetParameterProperties**方法将返回相同的错误代码与核心 OLE DB **icommandproperties:: Getproperties**方法中的，除 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED 之外不能为引发。  
  
## <a name="remarks"></a>备注  
 **Isscommandwithparameters:: Getparameterproperties**相对于一致的行为**GetParameterInfo**。 如果[isscommandwithparameters:: Setparameterproperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)或**SetParameterInfo**尚未调用或使用等于零的 cParams 调用了**GetParameterInfo**中派生参数信息并返回此信息。 如果**isscommandwithparameters:: Setparameterproperties**或**SetParameterInfo**已为至少一个参数调用**isscommandwithparameters:: Getparameterproperties**为其返回仅为这些参数的属性**isscommandwithparameters:: Setparameterproperties**已调用。 如果**isscommandwithparameters:: Setparameterproperties**后，会调用**isscommandwithparameters:: Getparameterproperties**或**GetParameterInfo**，对后续调用**isscommandwithparameters:: Getparameterproperties**重写这些参数的值返回为其**isscommandwithparameters:: Setparameterproperties**已调用。  
  
 SSPARAMPROPS 结构的定义如下所示：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|成员|描述|  
|------------|-----------------|  
|iOrdinal |所传递参数的序号。|  
|*cPropertySets*|rgPropertySets 中 DBPROPSET 结构的数量  。|  
|*rgPropertySets*|指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
  
## <a name="see-also"></a>请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
