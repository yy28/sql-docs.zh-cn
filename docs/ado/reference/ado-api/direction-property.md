---
title: "方向属性 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a81c60a4505e1c5e420583c474109d0d08f4fb6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="direction-property"></a>方向属性
指示是否[参数](../../../ado/reference/ado-api/parameter-object.md)表示输入的参数、 输出参数、 输入和输出参数，或如果参数是存储过程的返回值。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值。  
  
## <a name="remarks"></a>注释  
 使用**方向**属性来指定如何参数被传递到或从过程。 **方向**属性为读/写; 这样，你与不返回此信息的提供商合作或设置此信息时，你不希望 ADO 进行额外调用提供程序以检索参数信息。  
  
 并非所有提供程序可以确定其存储的过程中的参数的方向。 在这些情况下，你必须设置**方向**之前执行查询的属性。  
  
## <a name="applies-to"></a>适用范围  
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

