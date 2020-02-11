---
title: MarshalOptions 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0212f3b4cb663bd56adaa1bdbc3ab6675c3ce888
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932270"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions 属性 (ADO)
指示要将[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)封送回服务器的记录。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)值。 默认值为**adMarshalAll**。  
  
## <a name="remarks"></a>备注  
 使用客户端[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)时，已在客户端上修改的记录会通过一种称为封送的技术写回中间层或 Web 服务器，这是跨线程或进程边界打包和发送接口方法参数的过程。 设置**MarshalOptions**属性可以在将修改的远程数据封送回中间层或 Web 服务器时提高性能。  
  
> [!NOTE]
>  **远程数据服务使用情况**此属性仅在客户端**记录集**上使用。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [MarshalOptions 属性示例（VB）](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [MarshalOptions 属性示例 (VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
