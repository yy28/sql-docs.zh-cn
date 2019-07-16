---
title: 处理失败的更新 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d442a9c397ad184658f9101343e139697c9b3756
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925638"
---
# <a name="dealing-with-failed-updates"></a>处理失败的更新
如果更新由于错误而停止，如何解决这些错误依赖于的性质和错误的严重性和你的应用程序的逻辑。 但是，如果与其他用户共享的数据库，典型的错误是其他人在执行操作之前来修改字段。 这种类型的错误称为冲突。 ADO 检测到这种情况下，会报告错误。  
  
## <a name="remarks"></a>备注  
 如果更新错误，它们将被限制在错误处理例程中。 筛选与 adFilterConflictingRecords 常量记录集，以便仅冲突的行是可见的。 在此示例中，错误解决策略是只是打印作者的第一个和最后一个名称 （au_fname 和 au_lname）。  
  
 更新冲突向用户发出警报的代码如下所示：  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)
