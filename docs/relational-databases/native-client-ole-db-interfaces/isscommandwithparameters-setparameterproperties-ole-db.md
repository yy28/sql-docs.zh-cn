---
title: 'Isscommandwithparameters:: Setparameterproperties (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ccbc15cd4493f4d0d9654e9da130ac192f9f8c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416916"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  按照序号基于每个参数设置参数属性，或者通过指定 SSPARAMPROPS 结构数组来设置大容量参数属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>参数  
 *cParams*[in]  
 结构中的数量 SSPARAMPROPS *rgParamProperties*数组。 如果此数字为零， **isscommandwithparameters:: Setparameterproperties**将删除已为命令中的任何参数指定的所有属性。  
  
 *rgParamProperties*[in]  
 要设置的 SSPARAMPROPS 结构数组。  
  
## <a name="return-code-values"></a>返回代码值  
 **Isscommandwithparameters:: Setparameterproperties**方法将返回相同的错误代码与核心 OLE DB **icommandproperties:: Setproperties**方法。  
  
## <a name="remarks"></a>Remarks  
 使用此方法设置参数属性上允许，每个参数的序号，或使用单个**isscommandwithparameters:: Setparameterproperties**从属性数组生成 SSPARAMPROPS 之后调用。  
  
 **SetParameterInfo**调用之前，必须调用方法**isscommandwithparameters:: Setparameterproperties**方法。 调用 `SetParameterProperties(0, NULL)` 可清除所有指定的参数属性，而调用 `SetParameterInfo(0,NULL,NULL)` 则会清除所有参数信息（包括可能与某个参数相关的任何属性）。  
  
 调用**isscommandwithparameters:: Setparameterproperties**来指定参数的类型不是属性 DBTYPE_XML 或 DBTYPE_UDT 将返回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，并*dwStatus*使用 dbpropstatus_notset 标记该参数的 SSPARAMPROPS 中包含的所有 Dbprop 字段。 应当遍历 SSPARAMPROPS 中包含的每个 DBPROPSET 的 DBPROP 数组，以检测 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 引用了哪些参数。  
  
 如果**isscommandwithparameters:: Setparameterproperties**调用以指定的参数与，尚未尚未设置其参数信息的属性**SetParameterInfo**，访问接口将返回 E_意外的以下错误消息：  
  
 在没有先调用 SetParameterInfo 方法的情况下，不能为指定参数调用 SetParameterProperties 方法。 在设置参数属性之前，必须首先设置参数信息。  
  
 如果在调用**isscommandwithparameters:: Setparameterproperties**包含参数信息已设置，某些参数和某些参数的参数信息尚未设置中的 dwStatus 属性SSPARAMPROPS 属性集的 DBPROPSET 将返回带有 DBSTATUS_NOTSET。  
  
 SSPARAMPROPS 结构的定义如下所示：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 isscommandwithparameters:: Setparameterproperties 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 isscommandwithparameters:: Setparameterproperties 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../../relational-databases/native-client/features/metadata-discovery.md)。  
  
|成员|Description|  
|------------|-----------------|  
|*iOrdinal*|所传递参数的序号。|  
|*cPropertySets*|结构中的数量 DBPROPSET *rgPropertySets*。|  
|*rgPropertySets*|指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
  
## <a name="see-also"></a>请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
