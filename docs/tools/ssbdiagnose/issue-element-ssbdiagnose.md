---
title: "Issue 元素 (ssbdiagnose) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssbdiagnose
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 370b4d10d7a0b7bb9407ad6867d2c81de3ecda61
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="issue-element-ssbdiagnose"></a>Issue 元素 (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]发现了问题只报告**ssbdiagnose**实用程序。 在 **ssbdiagnose** XML 输出文件中，所报告的每个问题都有一个 Issue 元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|**type**|标识 Issue 元素报告的问题类别：<br /><br /> **“诊断”** 报告在分析 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 配置时发现的配置问题。<br /><br /> “问题” 报告阻止 **ssbdiagnose** 完成其分析的问题。 更正问题并重新运行 **ssbdiagnose**。<br /><br /> **“事件”** 报告在运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -RUNTIME **检查时发现的** 事件。 仅当指定了 **-SHOWEVENTS** 时才报告事件。|  
|**代码**|标识消息的错误号。|  
|**服务器**|标识在其中发现了问题的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例。 如果问题在默认实例中，则服务器属性只具有计算机名称。 如果问题在命名实例中，则服务器属性的格式为 ComputerName\InstanceName。|  
|**database**|标识在其中发现了问题的数据库的名称。|  
|**对象 (object)**|标识在其中发现了问题的对象的名称。 如果问题为实例或数据库级别的问题，则对象属性将重复该实例或数据库名称。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|**string**，无限长。|  
|**值**|返回错误消息的文本。|  
|**出现次数**|每个报告错误一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素 (ssbdiagnose)](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|无|  
  
## <a name="example"></a>示例  
 此元素报告没有主密钥的数据库的 1102 错误，分析 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 配置时在该数据库中发现了错误。  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>另请参阅  
 [ssbdiagnose 实用工具 (Service Broker)](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
