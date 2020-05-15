---
title: 服务器的数据库元素 (DTA)
description: 在 dta 实用工具中，服务器的 Database 元素指定要在特定服务器上优化的数据库。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: d416f6f57d70674a8f9a7b484f7da9c87b18342c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831584"
---
# <a name="database-element-for-server-dta"></a>服务器的数据库元素 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

指定特定服务器上要优化的数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无。|  
|默认值|无。|  
|出现次数|对于每个 **Server** 元素需要使用一次或多次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|父元素|[服务器元素 (DTA)](../../tools/dta/server-element-dta.md)|  
|子元素|[数据库的名称元素 (DTA)](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [数据库的架构元素 (DTA)](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>备注  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseDetailsTypecomplexType** 。 请不要将此 **Database** 元素与根级父元素为 **Configuration** 元素的元素相混淆。 有关详细信息，请参阅[用于配置的数据库元素 (DTA)](../../tools/dta/database-element-for-configuration-dta.md)。  
  
## <a name="example"></a>示例  
 有关 **Database** 元素的用法示例，请参阅 [服务器元素 (DTA)](../../tools/dta/server-element-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
