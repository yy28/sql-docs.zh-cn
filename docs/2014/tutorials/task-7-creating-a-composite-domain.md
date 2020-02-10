---
title: 任务7：创建复合域 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbc00117e10e48adbde37b9f0561610feff8f87e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65488967"
---
# <a name="task-7-creating-a-composite-domain"></a>任务 7：创建复合域规则
  在此任务中，你将创建一个包含**地址行**、**城市**、省/市/**自治区**和**Zip**域的复合域**地址验证**。 通过复合域，您可以定义在一个规则中涉及多个域的跨域规则。 复合域还有其他一些好处，例如能够将一个字段值分析到多个域中。  例如，可以将“全名”字段的值分析到单独的“名字”、“中间名”和“姓氏”域中。 在本教程中，您将只定义一个跨域规则。 有关更多详细信息，请参阅[管理复合域](https://msdn.microsoft.com/library/hh510399.aspx)。  
  
1.  在左侧窗格中，单击工具栏上的 "**创建复合域**" 按钮。  
  
     ![“创建复合域”工具栏按钮](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "“创建复合域”工具栏按钮")  
  
2.  输入**复合域名**的**地址验证**。  
  
     ![地址验证复合域](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "地址验证复合域")  
  
3.  从 "域" 列表中，选择 "**地址行**"、"**城市**"、"省/市/**自治区**" 和 " **Zip** "，然后单击**向右箭头**将其添加到 "**复合域**  
  
4.  单击 **“确定”** 关闭对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 8：创建复合域规则](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
