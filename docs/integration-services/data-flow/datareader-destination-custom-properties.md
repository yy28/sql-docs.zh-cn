---
title: DataReader 目标自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9394139b6085fc4f5d59a8202503f6c9e3d750f1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916740"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 目标自定义属性

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  DataReader 目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了 DataReader 目标的自定义属性。 除 **DataReader** 以外的所有属性均可读/写。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 目标的类名。|  
|FailOnTimeout|Boolean|指示发生 **ReadTimeout** 时是否失败。 此属性的默认值为 **False**。|  
|ReadTimeout|Integer|超时发生之前的毫秒数。 此属性的默认值为 30000（30 秒）。|  
  
 DataReader 目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [DataReader Destination](../../integration-services/data-flow/datareader-destination.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
