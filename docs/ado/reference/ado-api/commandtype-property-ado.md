---
title: CommandType 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cd6d06a50047f431700af9418a504faa4bd6957
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919694"
---
# <a name="commandtype-property-ado"></a>CommandType 属性 (ADO)
指示[命令](../../../ado/reference/ado-api/command-object-ado.md)对象的类型。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个或多个[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值。  
  
> [!NOTE]
>  不要将**adCmdFile**或**adCmdTableDirect**的**CommandTypeEnum**值与**CommandType**一起使用。 这些值只能用作[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)和重新[查询](../../../ado/reference/ado-api/requery-method.md)方法的选项。  
  
## <a name="remarks"></a>备注  
 使用**CommandType**属性优化[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性的计算。  
  
 如果**CommandType**属性值设置为默认值**adCmdUnknown**，则可能会遇到性能降低的情况，因为 ADO 必须对访问接口进行调用，以确定**CommandText**属性是否为 SQL 语句、存储过程或表名。 如果你知道要使用哪种类型的命令，则设置**CommandType**属性将指示 ADO 直接跳到相关代码。 如果**CommandType**属性与**CommandText**属性中的命令类型不匹配，则在调用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法时会发生错误。  
  
## <a name="applies-to"></a>应用于  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 属性示例（VB）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 属性示例（VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 属性示例（JScript）](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
