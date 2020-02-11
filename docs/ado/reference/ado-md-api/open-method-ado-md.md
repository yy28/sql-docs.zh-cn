---
title: Open 方法（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 089fad427989c26ed1ed22ec3e9267297a29b820
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949380"
---
# <a name="open-method-ado-md"></a>Open 方法 (ADO MD)
检索多维查询的结果，并将结果返回到[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>parameters  
 *数据源*  
 可选。 计算结果为有效多维查询的**变量**，如多维表达式（MDX）查询。 *Source*参数对应于[source](../../../ado/reference/ado-md-api/source-property-ado-md.md)属性。 有关 MDX 的详细信息，请参阅 Microsoft 数据访问组件 SDK 中的[联机分析处理（OLAP）的 OLE DB](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3)文档。  
  
 *ActiveConnection*  
 可选。 一个**变量**，其计算结果为字符串，该字符串指定有效的 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象变量名称或连接定义。 *ActiveConnection*参数指定要在其中打开[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象的连接。 如果传递此参数的连接定义，ADO 将使用指定的参数打开新连接。 *ActiveConnection*参数对应于[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)属性。  
  
## <a name="remarks"></a>备注  
 如果在尝试打开**单元集**之前省略了其参数的任何一个参数并且尚未设置其相应的属性值，则**Open**方法会生成错误。  
  
## <a name="applies-to"></a>应用于  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [单元集示例（VB）](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection 属性（ADO MD）](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close 方法（ADO MD）](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Connection 对象（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Source 属性（ADO MD）](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State 属性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
