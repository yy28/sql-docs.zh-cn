---
title: 原始文件自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b115edd3e8addbedc60c0c37b4ea014a3123909
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098217"
---
# <a name="raw-file-custom-properties"></a>原始文件自定义属性
  **源自定义属性**  
  
 原始文件源具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍原始文件源的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer（枚举）|用来访问原始数据的模式。 可能的值为 `File name` (0) 和 `File name from variable` (1)。 默认值为 `File name` (0)。|  
|FileName|String|源文件的路径和文件名。|  
  
 原始文件源的输出和输出列没有自定义属性。  
  
 有关详细信息，请参阅 [Raw File Source](raw-file-source.md)。  
  
 **目标自定义属性**  
  
 原始文件目标具有自定义属性和所有数据流组件通用的属性。  
  
 下表介绍了原始文件目标的自定义属性。 所有属性均可读/写。  
  
|属性名称|数据类型|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer（枚举）|一个值，指定 FileName 属性是包含文件名还是包含变量（包含文件名）名。 选项为 `File name` (0) 和 `File name from variable` (1)。|  
|FileName|String|原始文件目标要写入的文件的名称。|  
|WriteOption|Integer（枚举）|一个指定原始文件目标是否删除具有相同名称的现有文件的值。 选项包括`Create Always`(0)， `Create Once` (1)， `Truncate and Append` (3) 和`Append`(2)。 此属性的默认值是`Create Always`(0)。|  
  
> [!NOTE]  
>  追加操作要求追加数据的元数据与文件中已有数据的元数据匹配。  
  
 原始文件目标的输入和输入列没有自定义属性。  
  
 有关详细信息，请参阅 [Raw File Destination](raw-file-destination.md)。  
  
## <a name="see-also"></a>请参阅  
 [Common Properties](../common-properties.md)  
  
  
