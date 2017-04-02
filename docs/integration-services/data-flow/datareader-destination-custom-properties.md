---
title: "DataReader 目标自定义属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# DataReader 目标自定义属性
  DataReader 目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了 DataReader 目标的自定义属性。 除 **DataReader** 以外的所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|DataReader|字符串|DataReader 目标的类名。|  
|FailOnTimeout|Boolean|指示发生 **ReadTimeout** 时是否失败。 此属性的默认值为 **False**。|  
|ReadTimeout|Integer|超时发生之前的毫秒数。 此属性的默认值为 30000（30 秒）。|  
  
 DataReader 目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [DataReader Destination](../../integration-services/data-flow/datareader-destination.md)。  
  
## 另请参阅  
 [通用属性](../Topic/Common%20Properties.md)  
  
  