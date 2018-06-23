---
title: 任务 7： 创建复合域 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e88fa44fb4457a979dfa1236531ed8bfa61f88fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128006"
---
# <a name="task-7-creating-a-composite-domain"></a>任务 7：创建复合域规则
  在此任务中，创建复合域，**地址验证**，其包含**地址行**，**城市**，**状态**，和**Zip**域。 通过复合域，您可以定义在一个规则中涉及多个域的跨域规则。 复合域还有其他一些好处，例如能够将一个字段值分析到多个域中。  例如，可以将“全名”字段的值分析到单独的“名字”、“中间名”和“姓氏”域中。 在本教程中，您将只定义一个跨域规则。 请参阅[Managing a Composite Domain](http://msdn.microsoft.com/library/hh510399.aspx)有关详细信息。  
  
1.  在左窗格中，单击**创建复合域**工具栏上的按钮。  
  
     ![创建复合域工具栏按钮](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "创建复合域工具栏按钮")  
  
2.  输入**地址验证**为**复合域名**。  
  
     ![解决验证复合域](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "地址验证复合域")  
  
3.  从域列表中选择**地址行**，**城市**，**状态**，和**Zip**单击**右箭头**若要将其添加到**复合域中**列表。  
  
4.  单击 **“确定”** 关闭对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 8：创建复合域规则](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  