---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ceca46260d82cc6f9a179a642821aee55e57d6e3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429986"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)。 这是一个可选接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了三个方法继承自**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，并**SetParameterInfo**;**ISSCommandWithParameters**提供用于处理服务器特定的数据类型的两种新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**时使用服务组件，但是服务组件自身不会使用此接口，可以使用接口。  
  
|方法|Description|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|返回一个**SSPARAMPROPS**属性设置为传递到命令中，每个 UDT 或 XML 参数数组中的结构，但对于其他类型的参数返回 none。|  
|[Isscommandwithparameters:: Setparameterproperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|按照序号，基于每个参数设置参数属性或通过指定的数组来设置大容量参数属性**SSPARAMPROPS**结构。|  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [使用 XML 数据类型](../native-client/features/using-xml-data-types.md)   
 [使用用户定义类型](../native-client/features/using-user-defined-types.md)  
  
  
