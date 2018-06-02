---
title: 方法 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15f930695e13d824e70da748dad20cf574e9bc38
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579139"
---
# <a name="xml-elements---methods"></a>XML 元素的方法
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  XML for Analysis (XMLA) 协议使用两种方法，**发现**和**执行**，提供应用程序访问 Analysis Services 实例上的信息的标准方法。 由于这些方法是通过使用简单对象访问协议 (SOAP) 调用的，因此它们接受的输入和传递的输出都是 XML 格式。 Analysis Services 实现这两种方法，符合 XML for Analysis 1.1 规范。  
  
## <a name="in-this-section"></a>在本节中  
 以下主题介绍实现的 Analysis Services XMLA 方法。  
  
|方法|Description|  
|------------|-----------------|  
|[发现方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|从 Analysis Services 的实例中检索信息，如可用数据库或针对特定对象的详细信息的列表。 使用检索的数据**发现**方法取决于传递给它的参数的值。|  
|[执行方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|将 XMLA 命令发送到的 Analysis Services 实例。 这包括涉及数据传输的请求，如检索或更新服务器上的数据。|  
  
## <a name="see-also"></a>另请参阅
 [XML 元素&#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 数据类型&#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 元素&#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
