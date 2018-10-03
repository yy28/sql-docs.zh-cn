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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 67de6f79ceac48dc6e81ef9b61674fd65bd24bed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636995"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 目标自定义属性
  DataReader 目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了 DataReader 目标的自定义属性。 除 **DataReader** 以外的所有属性均可读/写。  
  
|属性名称|数据类型|描述|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 目标的类名。|  
|FailOnTimeout|Boolean|指示发生 **ReadTimeout** 时是否失败。 此属性的默认值为 **False**。|  
|ReadTimeout|Integer|超时发生之前的毫秒数。 此属性的默认值为 30000（30 秒）。|  
  
 DataReader 目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [DataReader Destination](../../integration-services/data-flow/datareader-destination.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
