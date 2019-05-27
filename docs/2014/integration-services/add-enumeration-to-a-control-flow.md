---
title: 将枚举添加到控制流 |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cad9c6a3537fb523a13f0206eed6c8eee837ed06
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061910"
---
# <a name="add-enumeration-to-a-control-flow"></a>将枚举添加到控制流
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含 Foreach 循环容器，此容器是一个控制流元素，利用它可以轻松地将枚举文件和对象的循环构造包括到包的控制流中。 有关详细信息，请参阅 [Foreach 循环容器](control-flow/foreach-loop-container.md)。  
  
 Foreach 循环容器不提供任何功能，只提供用以生成可重复的控制流、指定枚举器类型以及配置枚举器的结构。 若要提供容器功能，Foreach Loop 循环容器中必须包含至少一个任务。 有关详细信息，请参阅 [Integration Services Tasks](control-flow/integration-services-tasks.md)。  
  
 Foreach 循环容器可包含具有多个任务和其他容器的控制流。 除了要将任务和容器拖动到 Foreach 循环容器而不是拖放到包以外，将任务和容器添加到 Foreach 循环容器的过程与将其添加到包的过程相似。 如果 Foreach 循环容器包含多个任务或容器，可以使用优先约束连接它们，这与在包中的操作一样。 有关详细信息，请参阅 [优先约束](control-flow/precedence-constraints.md)。  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>在控制流中实现 Foreach 循环容器  
  
1.  将 Foreach 循环容器添加到包。 有关详细信息，请参阅[添加或删除任务或容器中控制流](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  将任务和容器添加到 Foreach 循环容器。 有关详细信息，请参阅[添加或删除任务或容器中控制流](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  使用优先约束连接 Foreach 循环容器中的任务和容器。 有关详细信息，请参阅 [使用默认优先约束来连接任务和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)。  
  
4.  配置 Foreach 循环容器。 有关详细信息，请参阅 [配置 Foreach 循环容器](../../2014/integration-services/configure-a-foreach-loop-container.md)。  
  
## <a name="see-also"></a>请参阅  
 [在控制流中添加或删除任务或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [组或取消分组的组件](group-or-ungroup-components.md)   
 [优先约束](control-flow/precedence-constraints.md)   
 [将迭代添加到控制流](add-iteration-to-a-control-flow.md)   
 [控制流](control-flow/control-flow.md)  
  
  
