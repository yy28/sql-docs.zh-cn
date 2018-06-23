---
title: DataReader 目标自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c7fb15f3dda170c866bb95840a7a3cde4c19ffa1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027722"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 目标自定义属性
  DataReader 目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了 DataReader 目标的自定义属性。 以外的所有属性`DataReader`读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 目标的类名。|  
|FailOnTimeout|Boolean|指示发生 `ReadTimeout` 时是否失败。 此属性的默认值为 **False**。|  
|ReadTimeout|Integer|超时发生之前的毫秒数。 此属性的默认值为 30000（30 秒）。|  
  
 DataReader 目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [DataReader Destination](datareader-destination.md)。  
  
## <a name="see-also"></a>请参阅  
 [Common Properties](../common-properties.md)  
  
  