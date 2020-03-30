---
title: 文件元素 (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- File element
ms.assetid: 73dce835-9a80-4aef-8e0f-9dcf07dd5b80
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 8c09dc0d2a4a31f63d0359fa7845dd37ff7e55fc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307685"
---
# <a name="file-element-dta"></a>文件元素 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

指定工作负荷文件。 工作负荷是对要优化的一个或多个数据库执行的一组 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 工作负荷文件可以是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件 (.sql)，也可以是跟踪文件 (.trc)。 有关详细信息，请参阅[启动并使用数据库引擎优化顾问](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
  <Server>...</Server>  
  <Workload>  
    <File>...</File>  
  </Workload>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|使用 **string** 数据类型，以指定工作负荷文件的目录路径。 例如：<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> 请注意，长度限制由服务器强制执行。|  
|**默认值**|无。|  
|**出现次数**|如果未指定其他类型的工作负荷，则必须使用一次。 必须为父元素 **EventString**指定子元素 **File**、 **Database** 或 **Workload** ，但只能使用一种类型。 例如，如果用 **文件** 元素指定工作负荷，则不能在同一 XML 输入文件中又用 **数据库** 元素指定工作负荷。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[工作负荷元素 (DTA)](../../tools/dta/workload-element-dta.md)|  
|**子元素**|无。|  
  
## <a name="example"></a>示例  
 有关该元素的使用示例，请参阅[简单 XML 输入文件示例 (DTA)](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
