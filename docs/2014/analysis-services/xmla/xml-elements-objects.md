---
title: 对象 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, objects
ms.assetid: 768188ef-85d4-432a-9390-be05c835137f
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 98ff50749cc45b5ffe4343acc19668f4dd0db126
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017607"
---
# <a name="objects-xmla"></a>对象 (XMLA)
  XML for Analysis (XMLA) 协议使用两种方法，`Discover`和`Execute`，提供应用程序访问的实例上的信息的标准方法[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 由于这些方法是使用简单对象访问协议 (SOAP) 调用的，因此它们接受 XML 格式的输入并传送 XML 格式的输出。  
  
## <a name="in-this-section"></a>本节内容  
 下面的主题介绍 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 实现的 XMLA 对象。  
  
|方法|Description|  
|------------|-----------------|  
|[DiscoverResponse 元素&#40;XMLA&#41;](xml-elements-objects-discoverresponse.md)|包含返回的实例的信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以响应[发现](xml-elements-methods-discover.md)方法调用。|  
|[ExecuteResponse 元素&#40;XMLA&#41;](xml-elements-objects-executeresponse.md)|包含返回的实例的信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以响应[执行](xml-elements-methods-execute.md)方法调用。|  
  
## <a name="see-also"></a>请参阅  
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [XML 数据类型&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [XML 元素&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  