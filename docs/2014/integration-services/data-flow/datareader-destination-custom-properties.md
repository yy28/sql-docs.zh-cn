---
title: DataReader 目标自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c7117115e461d0e33a3c62100a3e914128003b96
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790349"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 目标自定义属性
  DataReader 目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了 DataReader 目标的自定义属性。 除 `DataReader` 以外的所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 目标的类名。|  
|FailOnTimeout|Boolean|指示发生 `ReadTimeout` 时是否失败。 此属性的默认值为 **False**。|  
|ReadTimeout|Integer|超时发生之前的毫秒数。 此属性的默认值为 30000（30 秒）。|  
  
 DataReader 目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [DataReader Destination](datareader-destination.md)。  
  
## <a name="see-also"></a>请参阅  
 [Common Properties](../common-properties.md)  
  
  
