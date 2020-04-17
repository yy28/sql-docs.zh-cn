---
title: 配置用于循环容器 |微软文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 766a82c975b607687f79a696ce587422b93322bf
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486994"
---
# <a name="configure-a-for-loop-container"></a>配置 For 循环容器
  此过程介绍如何使用 **“For 循环编辑器”** 对话框配置 For 循环容器。  
  
### <a name="to-configure-the-for-loop-container"></a>配置 For 循环容器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，双击 For 循环容器，打开“For 循环编辑器”****。  
  
2.  根据需要，修改 For 循环容器的名称和说明。  
  
3.  根据需要，在 **InitExpression** 文本框中键入初始化表达式。  
  
4.  在 **EvalExpression** 文本框中键入求值表达式。  
  
    > [!NOTE]  
    >  表达式的计算结果必须为布尔值。 当表达式的计算结果为 `false` 时，循环停止运行。  
  
5.  根据需要，在 **AssignExpression** 文本框中键入赋值表达式。  
  
6.  根据需要，单击 **“表达式”** ，并在 **“表达式”** 页上为 For 循环容器的属性创建属性表达式。 有关详细信息，请参阅 [添加或更改属性表达式](expressions/add-or-change-a-property-expression.md)。  
  
7.  单击 **“确定”** ，关闭 **“For 循环编辑器”**。  
  
## <a name="see-also"></a>另请参阅  
 [用于循环容器](control-flow/for-loop-container.md)   
 [集成服务&#40;SSIS&#41;表达式](expressions/integration-services-ssis-expressions.md)   
 [在包中使用属性表达式](expressions/use-property-expressions-in-packages.md)  
  
  
