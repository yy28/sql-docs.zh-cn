---
title: 集合 (ADO for VisualC++语法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d94570a337f564588b2709fd292eab5ed5396dc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126698"
---
# <a name="collections-ado-for-visual-c-syntax"></a>集合（ADO for Visual C++ 语法）
## <a name="parameters"></a>Parameters  
  
### <a name="methods"></a>方法  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 有关详细信息，请参阅  
  
-   [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 方法（ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>属性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 有关详细信息，请参阅  
  
-   [Count 属性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 属性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>字段  
  
### <a name="methods"></a>方法  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 有关详细信息，请参阅  
  
-   [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 方法（ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>属性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 有关详细信息，请参阅  
  
-   [Count 属性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 属性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>错误  
  
### <a name="methods"></a>方法  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 有关详细信息，请参阅  
  
-   [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>属性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 有关详细信息，请参阅  
  
-   [Count 属性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 属性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>属性  
  
### <a name="methods"></a>方法  
  
```  
Refresh(void);  
```  
  
 有关详细信息，请参阅  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>属性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 有关详细信息，请参阅  
  
-   [Count 属性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 属性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [错误集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
