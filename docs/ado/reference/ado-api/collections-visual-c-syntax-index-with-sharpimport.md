---
description: '集合 (Visual C++ 语法索引与 #import 的) '
title: 集合 (#import) 的 Visual C++ 语法索引 |Microsoft Docs
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
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
author: rothja
ms.author: jroth
ms.openlocfilehash: e1e67827a5a496b6b9163d8fa8740cc620033efd
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776186"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>集合 (Visual C++ 语法索引与 #import 的) 
了解集合继承某些常用方法和属性很有用。  
  
 所有集合都继承 **Count** 属性和 **Refresh** 方法，所有集合都添加了 **Item** 属性。 **Errors**集合添加**Clear**方法。 **Parameters**集合继承了**append**和**delete**方法，而**字段**集合添加了**append**、 **delete**和**Update**方法。  
  
## <a name="properties-collection"></a>Properties 集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>属性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>错误集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>属性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Parameters 集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>属性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>字段集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>属性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>另请参阅  
 [ADO)  (收集 ](./errors-collection-ado.md)   
 [字段集合 (ADO) ](./fields-collection-ado.md)   
 [ADO) 的参数集合 (](./parameters-collection-ado.md)   
 [属性集合 (ADO)](./properties-collection-ado.md)