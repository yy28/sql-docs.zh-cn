---
title: 解析列引用编辑器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a16cf4e8307e2c6b09df18646c122459830d623e
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328041"
---
# <a name="resolve-column-reference-editor"></a>解析列引用编辑器
  在某一输入路径断开连接或者在该路径中存在任何未映射的列时，在相应的数据路径旁将显示一个错误图标。 为了简化列引用错误的解决方法，对于执行树中的所有路径，可以使用“解决引用”编辑器将未映射的输出列与未映射的输入列相链接。 “解决引用”编辑器还将突出显示路径以便指示正在解决的路径。  
  
> [!NOTE]  
>  即使在某一组件的输入路径断开连接时，也可以编辑该组件  
  
 在所有列引用都已解决后，如果没有任何其他数据路径错误，则在数据路径旁将不会显示错误图标。  
  
## <a name="options"></a>“常规”  
 **未映射的输出列（源）**    
 来自当前未映射的上游路径的列  
  
**映射的列（源）**    
 来自映射到下游路径中的列的上游路径的列  
  
**映射的列（目标）**    
 来自映射到下游路径中的列的上游路径的列  
  
**未映射的输入列（目标）**    
 来自当前未映射的下游路径的列  
  
**删除未映射的输入列**  
 选中“删除未映射的输入列”可以忽略数据路径目标处的未映射的列。 “预览更改”按钮显示在您按下“确定”按钮时将发生的更改的列表。  
  
  
