---
title: 工作负荷元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b2ff6e041783707a6c9a7fa5e2f4472fa8cd901a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315007"
---
# <a name="workload-element-dta"></a>工作负荷元素 (DTA)
  指定要用于优化会话的工作负荷。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|必须出现一次为每个`DTAInput`元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[启动并使用数据库引擎优化顾问](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**子元素**|[文件元素&#40;DTA&#41;](file-element-dta.md)<br /><br /> [工作负荷的数据库元素&#40;DTA&#41;](database-element-for-workload-dta.md)<br /><br /> [EventString 元素&#40;DTA&#41;](eventstring-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 工作负荷是对要优化的一个或多个数据库执行的一组 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 数据库引擎优化顾问可以将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本、跟踪文件和跟踪表用作工作负荷。  
  
 如果在 XML 输入文件中指定了一个工作负荷，同时又使用 **dta** 工具在命令行中指定了一个工作负荷，则将使用命令行中指定的工作负荷进行优化。 命令行中指定的所有优化选项的优先级均高于 XML 输入文件中指定的优化选项。 唯一的例外情况是：在计算模式下，在 XML 输入文件中输入用户指定的配置。 例如，如果在输入配置`Configuration`元素的 XML 输入文件和`EvaluateConfiguration`元素还指定为优化选项之一，则 XML 输入文件中指定的优化选项将覆盖在输入的任何优化选项命令行中。  
  
 必须为每个优化会话指定一个工作负荷。  
  
## <a name="example"></a>示例  
 下面的代码示例指定**MyDatabase.MyDBOwner.TuningTable001**跟踪表`Workload`元素。 使用带有 SQL Server 事件探查器的优化模板创建 **TuningTable001** ，并将该跟踪输出另存为一个表。  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
