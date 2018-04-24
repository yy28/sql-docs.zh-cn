---
title: 准备属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 452777c142b01b21a258e6f5432c48b243d45a40
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="prepared-property-ado"></a>已准备好的属性 (ADO)
指示是否要保存的已编译的版本[命令](../../../ado/reference/ado-api/command-object-ado.md)之前执行。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**布尔**值，如果设置为**True**，该值指示应准备命令。  
  
## <a name="remarks"></a>注释  
 使用**已准备**属性能够保存中指定的查询的已准备的 （或已编译的） 版本的提供程序[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性之前[命令](../../../ado/reference/ado-api/command-object-ado.md)对象的第一次执行。 这可能减慢命令的第一次执行，但后提供程序将编译命令，该提供程序将用于该命令的已编译的版本任何后续的执行，这将导致改进性能。  
  
 如果属性是**False**，提供程序将执行**命令**直接而无需创建的已编译的版本的对象。  
  
 如果提供程序不支持命令准备，当此属性设置为，它可能会返回错误**True**。 如果提供程序不返回错误，只需忽略请求后，若要准备的命令和集**已准备**属性**False**。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [已准备好的属性示例 (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 属性示例 (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
