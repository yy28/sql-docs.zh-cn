---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4ed73892ae0ebe88d4b18f2d2114143423570c60
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015417"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

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
 指向内存中将返回 SSPARAMPROPS 结构数组的位置的指针。 提供程序为结构分配内存并返回此内存的地址；当使用者不再需要这些结构时，可以使用 IMalloc::Free 释放该内存  。 在为 prgParamProperties 调用 IMalloc::Free 之前，使用者还必须为每个 DBPROP 结构的 vValue 属性调用 VariantClear，以防止当变量包含引用类型（如 BSTR）时发生内存泄漏     。 如果 pcParams 在输出时为零或者发生了 DB_E_ERRORSOCCURRED 之外的错误，则提供程序不分配任何内存，且确保 prgParamProperties 在输出时是一个空指针   。  
  
## <a name="return-code-values"></a>返回代码值  
 GetParameterProperties 方法返回与核心 OLE DB ICommandProperties::GetProperties 方法相同的错误代码，只是不引发 DB_S_ERRORSOCCURRED 和 DB_E_ERRORSOCCURED   。  
  
## <a name="remarks"></a>备注  
 对 GetParameterInfo 而言，ISSCommandWithParameters::GetParameterProperties 方法的行为一致   。 如果尚未调用 [ISSCommandWithParameters::SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 或 SetParameterInfo，或者未在 cParams 等于零时 调用它们，则 GetParameterInfo 将派生参数信息并返回此信息   。 如果至少已为一个参数调用了 ISSCommandWithParameters::SetParameterProperties 或 SetParameterInfo，则 ISSCommandWithParameters::GetParameterProperties 方法仅针对已对其调用 ISSCommandWithParameters::SetParameterProperties 的参数返回属性     。 如果在 ISSCommandWithParameters::GetParameterProperties 或 GetParameterInfo 之后调用 ISSCommandWithParameters::SetParameterProperties，则对 ISSCommandWithParameters::GetParameterProperties 的后续调用将针对已对其调用 ISSCommandWithParameters::SetParameterProperties 方法的参数返回重写的值      。  
  
 SSPARAMPROPS 结构的定义如下所示：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|成员|说明|  
|------------|-----------------|  
|iOrdinal |所传递参数的序号。|  
|cPropertySets |rgPropertySets 中 DBPROPSET 结构的数量  。|  
|rgPropertySets |指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
  
## <a name="see-also"></a>另请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
