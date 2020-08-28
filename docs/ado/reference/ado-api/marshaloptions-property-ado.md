---
description: MarshalOptions 属性 (ADO)
title: " (ADO) 的 MarshalOptions 属性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e7e574836f09df6f3bb8fdb078661c85cbf6355
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990668"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions 属性 (ADO)
指示要将 [记录集](./recordset-object-ado.md) 封送回服务器的记录。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 [MarshalOptionsEnum](./marshaloptionsenum.md) 值。 默认值为 **adMarshalAll**。  
  
## <a name="remarks"></a>注解  
 使用客户端 [记录集](./recordset-object-ado.md)时，已在客户端上修改的记录会通过一种称为封送的技术写回中间层或 Web 服务器，这是跨线程或进程边界打包和发送接口方法参数的过程。 设置 **MarshalOptions** 属性可以在将修改的远程数据封送回中间层或 Web 服务器时提高性能。  
  
> [!NOTE]
>  **远程数据服务使用情况** 此属性仅在客户端 **记录集**上使用。  
  
## <a name="applies-to"></a>适用于  
 [记录集对象 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [MarshalOptions 属性示例 (VB) ](./marshaloptions-property-example-vb.md)   
 [MarshalOptions 属性示例 (VC++)](./marshaloptions-property-example-vc.md)