---
description: Prepared 属性 (ADO)
title: ADO)  (已准备的属性 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b5095432d283a2a0695d948de08a9f6b0ab25c5
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773126"
---
# <a name="prepared-property-ado"></a>Prepared 属性 (ADO)
指示是否在执行前保存 [命令](./command-object-ado.md) 的已编译版本。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 **布尔** 值，如果设置为 **True**，则指示应准备好命令。  
  
## <a name="remarks"></a>备注  
 使用 "已**准备**" 属性可使提供程序在[命令](./command-object-ado.md)对象的第一次执行之前保存已准备的 (或已编译的查询) 版本。 [CommandText](./commandtext-property-ado.md) 这可能会减慢命令的第一次执行速度，但一旦提供程序编译了命令，提供程序就会将命令的编译版本用于后续执行，从而提高性能。  
  
 如果该属性为 **False**，则提供程序将直接执行 **命令** 对象而不创建已编译的版本。  
  
 如果提供程序不支持命令准备，则将此属性设置为 **True**时，它可能会返回错误。 如果提供程序未返回错误，则它只是忽略请求以准备命令并将 **准备** 的属性设置为 **False**。  
  
## <a name="applies-to"></a>适用于  
 [命令对象 (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [预定义的属性示例 (VB) ](./prepared-property-example-vb.md)   
 [Prepared 属性示例 (VC++)](./prepared-property-example-vc.md)