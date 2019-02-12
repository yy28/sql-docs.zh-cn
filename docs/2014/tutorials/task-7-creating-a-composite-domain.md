---
title: 任务 7:创建复合域 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c48144ca3720565c3c745ffd8aa39b0896e1fb66
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013788"
---
# <a name="task-7-creating-a-composite-domain"></a>任务 7:创建复合域
  在此任务中，创建复合域**地址验证**，其包含**Address Line**，**城市**，**状态**，和**Zip**域。 通过复合域，您可以定义在一个规则中涉及多个域的跨域规则。 复合域还有其他一些好处，例如能够将一个字段值分析到多个域中。  例如，可以将“全名”字段的值分析到单独的“名字”、“中间名”和“姓氏”域中。 在本教程中，您将只定义一个跨域规则。 请参阅[管理复合域](https://msdn.microsoft.com/library/hh510399.aspx)的更多详细信息。  
  
1.  在左窗格中，单击**创建复合域**工具栏上的按钮。  
  
     ![创建复合域工具栏按钮](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "创建复合域工具栏按钮")  
  
2.  输入**地址验证**有关**复合域名称**。  
  
     ![地址验证复合域](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "地址验证复合域")  
  
3.  从域列表中选择**Address Line**，**市/县**，**状态**，以及**Zip**单击**向右箭头**若要将其添加到**复合域中**列表。  
  
4.  单击 **“确定”** 关闭对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 8:创建复合域规则](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
