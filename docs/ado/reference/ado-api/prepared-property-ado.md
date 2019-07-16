---
title: 准备好属性 (ADO) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917591"
---
# <a name="prepared-property-ado"></a>Prepared 属性 (ADO)
指示是否要保存的已编译的版本[命令](../../../ado/reference/ado-api/command-object-ado.md)之前执行。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**布尔**值，如果设置为**True**，指示应准备命令。  
  
## <a name="remarks"></a>备注  
 使用**已准备**属性具有以下提供程序将准备就绪 （或已编译） 查询中指定的版本保存[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)之前属性[命令](../../../ado/reference/ado-api/command-object-ado.md)对象的第一次执行。 这样可能会降低命令的第一次执行，但后提供程序进行了编译命令，该提供程序将用于该命令的已编译的版本任何后续的执行，这将导致改进性能。  
  
 如果该属性是**False**，提供程序将执行**命令**直接而无需创建已编译的版本的对象。  
  
 如果提供程序不支持命令准备，此属性设置为时，它可能返回错误 **，则返回 True**。 如果提供程序不返回错误，只需忽略准备的命令和集请求**已准备**属性设置为**False**。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Prepared 的属性示例 (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 属性示例 (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
