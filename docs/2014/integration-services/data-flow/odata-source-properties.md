---
title: OData 源属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 26be406c26c362f1bd7fc5880e7c889fbd450ad6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915181"
---
# <a name="odata-source-properties"></a>OData 源属性
  在数据流中右键单击“OData 源”并单击“属性”时，将在“属性”窗口中看到“OData 源”组件的属性****************。  
  
|||  
|-|-|  
|属性|说明|  
|CollectionName|要从 OData 服务检索的集合的名称。 **“CollectionName”** 属性在 **UseResourcePath** 为 False 时使用。<br /><br /> 此属性能够使用表达式，从而可在运行时设置值。 但是，如果集合的元数据与设计时使用的元数据不匹配，会出现验证错误，从而导致数据流执行失败。|  
|DefaultStringLength|此值为没有最大长度的字符串列指定默认长度。<br /><br /> **默认值：** 4000|  
|查询|OData 查询参数。 此属性能够使用表达式，可以在运行时设置。|  
|ResourcePath|在需要指定完整资源路径（而不仅仅是选择集合名称）时使用此属性。 此属性在 **UseResourcePath** 为 True 时使用。|  
|UseResourcePath|设置为 True 时， **ResourcePath** 值追加到基 URL 以确定 OData 馈送位置。 设置为 False 时 ，使用 **CollectionName** 值。<br /><br /> **默认值：** False|  
  
  
