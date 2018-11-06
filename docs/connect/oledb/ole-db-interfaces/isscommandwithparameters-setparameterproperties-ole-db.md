---
title: 'Isscommandwithparameters:: Setparameterproperties (OLE DB) |Microsoft Docs'
description: ISSCommandWithParameters::SetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 8298de4362b0c38b56d56d7cbd46822a53b4ddbb
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030044"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  按照序号基于每个参数设置参数属性，或者通过指定 SSPARAMPROPS 结构数组来设置大容量参数属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>参数  
 cParams[in]  
 rgParamProperties 数组中 SSPARAMPROPS 结构的数量。 如果此数值为零，ISSCommandWithParameters::SetParameterProperties 将删除可能已经为该命令中的任何参数指定的所有属性。  
  
 rgParamProperties[in]  
 要设置的 SSPARAMPROPS 结构数组。  
  
## <a name="return-code-values"></a>返回代码值  
 ISSCommandWithParameters::SetParameterProperties 方法返回的错误代码与核心 OLE DB ICommandProperties::SetProperties 方法返回的错误代码相同。  
  
## <a name="remarks"></a>Remarks  
 允许按照序号基于每个参数使用此方法设置参数属性，或者在已经从属性数组生成 SSPARAMPROPS 之后使用单个 ISSCommandWithParameters::SetParameterProperties 调用设置参数属性。  
  
 在调用 ISSCommandWithParameters::SetParameterProperties 方法之前，必须首先调用 SetParameterInfo 方法。 调用 `SetParameterProperties(0, NULL)` 可清除所有指定的参数属性，而调用 `SetParameterInfo(0,NULL,NULL)` 则会清除所有参数信息（包括可能与某个参数相关的任何属性）。  
  
 对于不属于 DBTYPE_XML 类型或 DBTYPE_UDT 类型的参数，如果调用 ISSCommandWithParameters::SetParameterProperties 以指定相应参数的属性，将返回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，并使用 DBPROPSTATUS_NOTSET 标记该参数的 SSPARAMPROPS 中包含的所有 DBPROP 的 dwStatus 字段。 应当遍历 SSPARAMPROPS 中包含的每个 DBPROPSET 的 DBPROP 数组，以检测 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 引用了哪些参数。  
  
 如果调用 ISSCommandWithParameters::SetParameterProperties 以指定尚未使用 SetParameterInfo 设置其参数信息的参数的属性，访问接口将返回 E_UNEXPECTED 并显示以下错误消息：  
  
 在没有先调用 SetParameterInfo 方法的情况下，不能为指定参数调用 SetParameterProperties 方法。 在设置参数属性之前，必须首先设置参数信息。  
  
 如果对 ISSCommandWithParameters::SetParameterProperties 的调用包含某些参数，其中已设置了参数信息，而另一些参数未设置参数信息，则返回的 SSPARAMPROPS 属性集的 DBPROPSET 中的 dwStatus 属性将带有 DBSTATUS_NOTSET。  
  
 SSPARAMPROPS 结构的定义如下所示：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]允许 isscommandwithparameters:: Setparameterproperties 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 isscommandwithparameters:: Setparameterproperties 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../oledb/features/metadata-discovery.md)。  
  
|成员|描述|  
|------------|-----------------|  
|iOrdinal|所传递参数的序号。|  
|cPropertySets|rgPropertySets 中 DBPROPSET 结构的数量。|  
|rgPropertySets|指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
  
## <a name="see-also"></a>另请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
