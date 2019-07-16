---
title: 方向属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6135650d3b5cb015fad21d1eac7b350827965ca1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933079"
---
# <a name="direction-property"></a>Direction 属性
指示是否[参数](../../../ado/reference/ado-api/parameter-object.md)表示输入的参数、 输出参数、 输入和输出参数，或如果参数是存储过程的返回值。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)值。  
  
## <a name="remarks"></a>备注  
 使用**方向**属性指定一个参数传递到或从过程的方式。 **方向**属性为读/写，这使您能够提供程序不返回此信息的使用或来设置此信息时，您不希望 ADO 进行额外调用提供程序来检索参数信息。  
  
 并非所有提供程序可以确定他们的存储过程中的参数的方向。 在这些情况下，必须设置**方向**属性在执行查询之前。  
  
## <a name="applies-to"></a>适用范围  
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
