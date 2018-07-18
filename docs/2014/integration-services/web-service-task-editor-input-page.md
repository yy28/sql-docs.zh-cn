---
title: Web 服务任务编辑器 （输入页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.input.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 93529c88-f540-47f2-a10a-12c87318ed6f
caps.latest.revision: 29
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e6322a234ea1653f578f60b36a84b7e2c71af169
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264953"
---
# <a name="web-service-task-editor-input-page"></a>Web 服务任务编辑器（“输入”页）
  可以使用 **“Web 服务任务编辑器”** 对话框的 **“输入”** 页，指定 Web 服务、Web 方法和作为输入提供给 Web 方法的值。 可通过直接在“值”列中键入字符串或在“值”列中选择变量来提供这些值。  
  
 若要了解此任务，请参阅 [Web 服务任务](control-flow/web-service-task.md)。  
  
## <a name="options"></a>“常规”  
 **服务**  
 从列表中选择用来执行 Web 方法的 Web 服务。  
  
 **方法**  
 从列表中为要执行的任务选择 Web 方法。  
  
 **WebMethodDocumentation**  
 键入对 Web 方法的说明，或单击浏览按钮 **(…)**，再在“Web 方法文档”对话框中键入说明。  
  
 **名称**  
 列出为 Web 方法提供的输入名称。  
  
 **类型**  
 列出输入的数据类型。  
  
> [!NOTE]  
>  Web 服务任务仅支持以下数据类型的参数：Primitive 类型（如 integer 和 string）、Primitive 类型的数组和序列，以及枚举。  
  
 **变量**  
 选中该复选框以使用变量来提供输入。  
  
 **ReplTest1**  
 如果选中了“变量”复选框，则请在列表中选择要提供输入的变量；否则，请键入要在输入中使用的值。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Web 服务任务编辑器&#40;常规页&#41;](general-page-of-integration-services-designers-options.md)   
 [Web 服务任务编辑器&#40;输出页&#41;](../../2014/integration-services/web-service-task-editor-output-page.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
