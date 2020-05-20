---
title: Seek 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
author: rothja
ms.author: jroth
ms.openlocfilehash: a96c8054d83fa0ecff4cc3fed3a1227f300f7e2e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765398"
---
# <a name="seek-method"></a>Seek 方法
搜索[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的索引以快速找到与指定值匹配的行，并将当前行的位置更改为该行。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>参数  
 *架构*  
 **变量**值的数组。 索引由一个或多个列组成，数组包含一个要与每个对应列进行比较的值。  
  
 *SeekOption*  
 一个[SeekEnum](../../../ado/reference/ado-api/seekenum.md)值，指定要在索引的列和对应的*架构*之间进行的比较的类型。  
  
## <a name="remarks"></a>备注  
 如果基础提供程序支持**Recordset**对象上的索引，则将**Seek**方法与[Index](../../../ado/reference/ado-api/index-property.md)属性结合使用。 使用[支持](../../../ado/reference/ado-api/supports-method.md)**（adSeek）** 方法来确定基础提供程序是否支持**查找**，并使用**支持（a）** 方法来确定提供程序是否支持索引。 （例如， [Microsoft Jet 的 OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支持**查找**和**索引**。）  
  
 如果查找找不到所需的行 **，则不**会出现错误，并且行位于**记录集**的末尾。 执行此方法之前，请将**index**属性设置为所需的索引。  
  
 只有服务器端游标才支持此方法。 当**记录集**对象的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性值为**adUseClient**时，不支持查找。  
  
 仅当使用[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**打开**Recordset**对象时，才能使用此方法。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Seek 方法和 Index 属性示例（VB）](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Seek 方法和 Index 属性示例（VC + +）](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find 方法（ADO）](../../../ado/reference/ado-api/find-method-ado.md)   
 [Index 属性](../../../ado/reference/ado-api/index-property.md)
