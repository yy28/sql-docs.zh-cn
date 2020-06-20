---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: rothja
ms.author: jroth
ms.openlocfilehash: 295026497a97b4ce13d1a1a68de48079809390ad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056087"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters**公开对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 和用户定义类型（UDT）的支持。 这是一个可选接口，它继承自 core OLE DB interface **ICommandWithParameters**。 除了从**ICommandWithParameters**继承的三个方法;**GetParameterInfo**、 **MapParameterNames**和**SetParameterInfo**;**ISSCommandWithParameters**提供了两种新方法用于处理特定于服务器的数据类型。  
  
> [!NOTE]  
>  使用服务组件时，可以使用**ISSCommandWithParameters**接口，但服务组件本身将不会使用此接口。  
  
|方法|说明|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|对传递到该命令的每个 UDT 或 XML 参数返回数组中的一个 SSPARAMPROPS 属性集结构，但是对于其他类型的参数，不会返回任何内容****。|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|按照序号基于每个参数设置参数属性，或者通过指定 SSPARAMPROPS 结构数组来设置大容量参数属性****。|  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [使用 XML 数据类型](../native-client/features/using-xml-data-types.md)   
 [使用用户定义类型](../native-client/features/using-user-defined-types.md)  
  
  
