---
title: Open 方法 (ADO MD) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6fb508318c54e4b82a4efd301b889baadad6edc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="open-method-ado-md"></a>Open 方法 (ADO MD)
检索多维查询的结果，并返回到结果[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parameters  
 *数据源*  
 選擇性。 A **Variant**计算结果为有效的多维查询，例如多维表达式 (MDX) 查询。 *源*参数对应于[源](../../../ado/reference/ado-md-api/source-property-ado-md.md)属性。 有关 MDX 的详细信息，请参阅[OLE DB 的联机分析处理 (OLAP)](http://msdn.microsoft.com/en-us/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) Microsoft 数据访问组件 SDK 中的文档。  
  
 *ActiveConnection*  
 選擇性。 A **Variant**计算结果为一个字符串，请指定有效的 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象变量名或连接的定义。 *ActiveConnection*参数指定要在其中打开连接[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象。 如果您传入的连接定义为此参数，ADO 将打开一个新的连接，使用指定的参数。 *ActiveConnection*参数对应于[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)属性。  
  
## <a name="remarks"></a>注释  
 **打开**方法将生成错误，如果未指定的任一参数和及其对应的属性值未尝试打开之前设置**单元集**。  
  
## <a name="applies-to"></a>适用范围  
 [单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [单元集示例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection 属性 (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close 方法 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [源属性 (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State 属性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
