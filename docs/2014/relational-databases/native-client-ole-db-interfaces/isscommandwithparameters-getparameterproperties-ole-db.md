---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f06c97d1f6d1e477700117c3038d0186db085fd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024315"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
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
 指向内存中将返回 SSPARAMPROPS 结构数组的位置的指针。 提供程序为结构分配内存和的地址返回到此内存;使用者释放此内存， **IMalloc::Free**当不再需要两个结构。 之前调用**IMalloc::Free**为*prgParamProperties*，使用者还必须调用**VariantClear**为*vValue*属性为了防止内存泄漏，在其中将该变量包含的引用的情况下每个需要的 DBPROP 结构类型 （如 BSTR。)如果*pcParams*是零上的输出或发生 DB_E_ERRORSOCCURRED 其他错误，该提供程序不会分配任何内存，并确保*prgParamProperties*是输出的 null 指针。  
  
## <a name="return-code-values"></a>返回代码值  
 **GetParameterProperties**方法返回作为核心 OLE DB 相同的错误代码**ICommandProperties::GetProperties**方法，除非该 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED 不能为引发。  
  
## <a name="remarks"></a>Remarks  
 **ISSCommandWithParameters::GetParameterProperties**行为保持一致相对于**GetParameterInfo**。 如果[ISSCommandWithParameters::SetParameterProperties](isscommandwithparameters-setparameterproperties-ole-db.md)或**SetParameterInfo**尚未调用或与 cParams 等于零，调用了**GetParameterInfo**派生参数信息，并返回此。 如果**ISSCommandWithParameters::SetParameterProperties**或**SetParameterInfo**已调用至少一个参数， **ISSCommandWithParameters::GetParameterProperties**为其返回仅为这些参数的属性**ISSCommandWithParameters::SetParameterProperties**已调用。 如果**ISSCommandWithParameters::SetParameterProperties**后，会调用**ISSCommandWithParameters::GetParameterProperties**或**GetParameterInfo**，后续调用**ISSCommandWithParameters::GetParameterProperties**为其返回的这些参数的重写的值**ISSCommandWithParameters::SetParameterProperties**已调用。  
  
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
  
## <a name="see-also"></a>请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  