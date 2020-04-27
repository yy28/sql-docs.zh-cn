---
title: 已准备属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee7a94a06aa574c84c01cb8b9d05ebfcdf327d44
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917591"
---
# <a name="prepared-property-ado"></a>Prepared 属性 (ADO)
指示是否在执行前保存[命令](../../../ado/reference/ado-api/command-object-ado.md)的已编译版本。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**布尔**值，如果设置为**True**，则指示应准备好命令。  
  
## <a name="remarks"></a>备注  
 使用 "已**准备**" 属性可使提供程序在[命令](../../../ado/reference/ado-api/command-object-ado.md)对象的第一次执行之前保存在[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性中指定的已准备好的（或编译的）版本。 这可能会减慢命令的第一次执行速度，但一旦提供程序编译了命令，提供程序就会将命令的编译版本用于后续执行，从而提高性能。  
  
 如果该属性为**False**，则提供程序将直接执行**命令**对象而不创建已编译的版本。  
  
 如果提供程序不支持命令准备，则将此属性设置为**True**时，它可能会返回错误。 如果提供程序未返回错误，则它只是忽略请求以准备命令并将**准备**的属性设置为**False**。  
  
## <a name="applies-to"></a>应用于  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [已准备的属性示例（VB）](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 属性示例 (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
