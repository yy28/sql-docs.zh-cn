---
title: 'Isscommandwithparameters:: Setparameterproperties (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 778021ce007f0c1eac68197e0c07e2cb7b0bb001
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638772"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
  按照序号基于每个参数设置参数属性，或者通过指定 SSPARAMPROPS 结构数组来设置大容量参数属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>参数  
 *cParams*[in]  
 rgParamProperties 数组中 SSPARAMPROPS 结构的数量  。 如果此数字为零，`ISSCommandWithParameters::SetParameterProperties`将删除已为命令中的任何参数指定的所有属性。  
  
 *rgParamProperties*[in]  
 要设置的 SSPARAMPROPS 结构数组。  
  
## <a name="return-code-values"></a>返回代码值  
 `ISSCommandWithParameters::SetParameterProperties`方法将返回相同的错误代码与核心 OLE DB **icommandproperties:: Setproperties**方法。  
  
## <a name="remarks"></a>备注  
 使用此方法设置参数属性上允许，每个参数的序号，或使用单个`ISSCommandWithParameters::SetParameterProperties`从属性数组生成 SSPARAMPROPS 之后调用。  
  
 **SetParameterInfo**调用之前，必须调用方法`ISSCommandWithParameters::SetParameterProperties`方法。 调用 `SetParameterProperties(0, NULL)` 可清除所有指定的参数属性，而调用 `SetParameterInfo(0,NULL,NULL)` 则会清除所有参数信息（包括可能与某个参数相关的任何属性）。  
  
 调用`ISSCommandWithParameters::SetParameterProperties`来指定参数的类型不是属性 DBTYPE_XML 或 DBTYPE_UDT 将返回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，并*dwStatus* SSPARAMPROPS 中包含的所有 Dbprop 字段使用 dbpropstatus_notset 标记该参数。 应当遍历 SSPARAMPROPS 中包含的每个 DBPROPSET 的 DBPROP 数组，以检测 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 引用了哪些参数。  
  
 如果`ISSCommandWithParameters::SetParameterProperties`调用以指定的参数与，尚未尚未设置其参数信息的属性**SetParameterInfo**，访问接口将返回 E_UNEXPECTED 并显示以下错误消息：  
  
 在没有先调用 SetParameterInfo 方法的情况下，不能为指定参数调用 SetParameterProperties 方法。 在设置参数属性之前，必须首先设置参数信息。  
  
 如果在调用`ISSCommandWithParameters::SetParameterProperties`包含一些参数，其中已设置参数信息，并且其中尚未设置参数信息，某些参数的 SSPARAMPROPS 属性集的 DBPROPSET 中的 dwStatus 属性将返回带有 DBSTATUS_NOTSET。  
  
 SSPARAMPROPS 结构的定义如下所示：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 isscommandwithparameters:: Setparameterproperties 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 isscommandwithparameters:: Setparameterproperties 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
|成员|Description|  
|------------|-----------------|  
|iOrdinal |所传递参数的序号。|  
|*cPropertySets*|rgPropertySets 中 DBPROPSET 结构的数量  。|  
|*rgPropertySets*|指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
  
## <a name="see-also"></a>请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
