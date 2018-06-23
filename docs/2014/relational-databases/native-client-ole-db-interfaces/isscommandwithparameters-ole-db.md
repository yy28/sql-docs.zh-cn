---
title: ISSCommandWithParameters (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 90359b753baff55d70c00727b8230c41059ceaa3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029224"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和用户定义类型 (UDT)。 这是一个可选接口继承自核心 OLE DB 接口**ICommandWithParameters**。 除了从继承的三个方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供用于处理服务器特定的数据类型的两种新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**时使用了服务组件，但服务组件本身将不使用此接口，可以使用接口。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|返回一个**SSPARAMPROPS**属性设置为传递到命令中，每个 UDT 或 XML 参数数组中的结构，但对于其他类型的参数返回 none。|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|序号，基于每个参数设置参数属性或通过指定的数组设置大容量参数属性**SSPARAMPROPS**结构。|  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [使用 XML 数据类型](../native-client/features/using-xml-data-types.md)   
 [使用用户定义类型](../native-client/features/using-user-defined-types.md)  
  
  