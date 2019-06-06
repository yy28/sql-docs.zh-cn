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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 21cb7f8773c0663d584f62bcaaaeab15c7eac108
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711431"
---
# <a name="seek-method"></a>Seek 方法
搜索的索引[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)快速找到匹配指定的值，并将更改为该行的当前行位置的行。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>Parameters  
 *KeyValues*  
 一个数组**变体**值。 索引的一个或多个列组成，该数组包含要与每个对应列进行比较的值。  
  
 *SeekOption*  
 一个[SeekEnum](../../../ado/reference/ado-api/seekenum.md)值，该值指定要进行索引的列与相应之间的比较类型*架构*。  
  
## <a name="remarks"></a>备注  
 使用**Seek**方法一起[索引](../../../ado/reference/ado-api/index-property.md)如果基础提供程序上支持索引属性**记录集**对象。 使用[支持](../../../ado/reference/ado-api/supports-method.md) **(adSeek)** 方法，以确定基础提供程序是否支持**搜寻**，以及**Supports(adIndex)** 若要确定该提供程序是否支持索引的方法。 (例如， [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支持**Seek**并**索引**。)  
  
 如果**Seek**不找到所需的行中，没有错误发生，而且行位于末尾处**记录集**。 设置**索引**之前执行此方法所需索引的属性。  
  
 使用服务器端游标仅支持此方法。 查找时不支持**记录集**对象的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性值是**adUseClient**。  
  
 此方法仅可使用时**记录集**以打开对象[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)的值**adCmdTableDirect**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Seek 方法和 Index 属性示例 (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Seek 方法和 Index 属性示例 （VC + +）](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Index 属性](../../../ado/reference/ado-api/index-property.md)
