---
title: ISSCommandWithParameters::SetParameterProperties (OLE DB) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
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
 cParams[in]**  
 rgParamProperties 数组中 SSPARAMPROPS 结构的数量**。 如果此数为零， `ISSCommandWithParameters::SetParameterProperties`则将删除可能已为命令中的任何参数指定的所有属性。  
  
 rgParamProperties[in]**  
 要设置的 SSPARAMPROPS 结构数组。  
  
## <a name="return-code-values"></a>返回代码值  
 `ISSCommandWithParameters::SetParameterProperties`方法返回与 Core OLE DB **ICommandProperties：： SetProperties**方法相同的错误代码。  
  
## <a name="remarks"></a>备注  
 使用此方法设置参数属性的方法是按顺序在每个参数基础上使用，也`ISSCommandWithParameters::SetParameterProperties`可以在从属性数组生成 SSPARAMPROPS 后使用单个调用。  
  
 在**SetParameterInfo**调用`ISSCommandWithParameters::SetParameterProperties`方法之前，必须调用 SetParameterInfo 方法。 调用 `SetParameterProperties(0, NULL)` 可清除所有指定的参数属性，而调用 `SetParameterInfo(0,NULL,NULL)` 则会清除所有参数信息（包括可能与某个参数相关的任何属性）。  
  
 调用`ISSCommandWithParameters::SetParameterProperties`以指定参数的属性，该参数的类型不是 DBTYPE_XML 或 DBTYPE_UDT 返回 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED，并使用 DBPROPSTATUS_NOTSET 标记该参数包含在 SSPARAMPROPS 中的所有 Dbprop 的*dwStatus*字段。 应当遍历 SSPARAMPROPS 中包含的每个 DBPROPSET 的 DBPROP 数组，以检测 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 引用了哪些参数。  
  
 如果`ISSCommandWithParameters::SetParameterProperties`调用以指定参数信息尚未使用**SetParameterInfo**设置的参数的属性，则提供程序将返回 E_UNEXPECTED，并返回以下错误消息：  
  
 在没有先调用 SetParameterInfo 方法的情况下，不能为指定参数调用 SetParameterProperties 方法。 在设置参数属性之前，必须首先设置参数信息。  
  
 如果对`ISSCommandWithParameters::SetParameterProperties`的调用包含某些参数信息已设置的参数，而某些参数尚未设置参数信息，则 SSPARAMPROPS 属性集的 DBPROPSET 中的 dwStatus 属性将返回 DBSTATUS_NOTSET。  
  
 SSPARAMPROPS 结构的定义如下所示：  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 自 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 起，借助数据库引擎中的改进，ISSCommandWithParameters::SetParameterProperties 可以获取预期结果的更准确描述。 这些更准确的结果可能与旧版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 ISSCommandWithParameters::SetParameterProperties 返回的值有所不同。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
|成员|说明|  
|------------|-----------------|  
|iOrdinal**|所传递参数的序号。|  
|cPropertySets**|rgPropertySets 中 DBPROPSET 结构的数量**。|  
|rgPropertySets**|指向内存中将返回 DBPROPSET 结构数组的位置的指针。|  
  
## <a name="see-also"></a>另请参阅  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
