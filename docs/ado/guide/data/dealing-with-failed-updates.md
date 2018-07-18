---
title: 处理失败的更新 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e5a20e0527f8b30035aef7ff86a90378039b69
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270186"
---
# <a name="dealing-with-failed-updates"></a>处理失败的更新
当更新到结束但出现错误时，则如何解决这些错误取决的性质和错误的严重性和你的应用程序的逻辑。 但是，如果数据库已与其他用户共享的则典型的错误是其他人在你开始前修改字段。 此类型的错误称为冲突。 ADO 检测到这种情况下，会报告错误。  
  
## <a name="remarks"></a>Remarks  
 如果不存在更新错误，则它们将被限制在错误处理例程中。 筛选与 adFilterConflictingRecords 常量记录集，以便仅的冲突行可见。 在此示例中，错误解决策略是仅打印作者的名字和姓氏 （au_fname 和 au_lname） 的名称。  
  
 更新冲突向用户发出警报的代码如下所示：  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)
