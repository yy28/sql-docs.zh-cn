---
title: "解析列引用编辑器 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2ff8a97d45d75c3e93d4aa3111b653c9612b889
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="resolve-column-reference-editor"></a>解析列引用编辑器
  在某一输入路径断开连接或者在该路径中存在任何未映射的列时，在相应的数据路径旁将显示一个错误图标。 若要简化列引用错误的解决方法，解决引用编辑器，可链接的执行树中的所有路径未映射的输入列未映射的输出列。 “解决引用”编辑器还将突出显示路径以便指示正在解决的路径。  
  
> [!NOTE]  
>  可以编辑某一组件，即使其输入的路径断开连接  
  
 在所有列引用都已解决后，如果没有任何其他数据路径错误，则在数据路径旁将不会显示错误图标。  
  
## <a name="options"></a>选项  
 **未映射的输出列 （源）**    
 来自当前未映射的上游路径的列  
  
**映射的列 （源）**    
 来自映射到下游路径中的列的上游路径的列  
  
**映射的列 （目标）**    
 来自映射到下游路径中的列的上游路径的列  
  
**未映射的输入的列 （目标）**    
 来自当前未映射的下游路径的列  
  
**删除未映射的输入列**  
 选中“删除未映射的输入列”可以忽略数据路径目标处的未映射的列。 “预览更改”按钮显示在您按下“确定”按钮时将发生的更改的列表。  
  
  

