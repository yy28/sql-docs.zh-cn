---
title: "警报属性 - 新建警报（“响应”页）| Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8714981cdc2c8135597a253a15753730c0e523c0
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="alert-properties---new-alert-response-page"></a>警报属性 - 新建警报（“响应”页）
使用此页可以指定要运行的某项作业，并可获取为响应 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理警报而接收相关通知的操作员列表。  
  
## <a name="options"></a>选项  
**执行作业**  
启用“作业列表”、“新建作业”和“查看作业”选项。  
  
**新建作业**  
打开“新建作业”对话框。 此按钮在“执行作业”处于未选中状态时不可用。  
  
**查看作业**  
查看或修改所选作业。 此选项在“执行作业”处于未选中状态时不可用。  
  
**通知操作员**  
启用可用来添加、删除或更改操作员的控件。  
  
**操作员列表**  
列出在发生警报时要获得通知的操作员。 若要指定通知方法，请选中显示在操作员姓名后面的“电子邮件”、“寻呼程序”或“Net send”复选框。此选项在“通知操作员”处于未选中状态时不可用。  
  
**电子邮件**  
使用电子邮件通知操作员。  
  
**寻呼程序**  
使用寻呼电子邮件地址通知操作员。  
  
**Net send**  
使用 **net send** 通知操作员。  
  
**新建操作员**  
显示可用于创建新操作员的“新建操作员”对话框。  
  
**查看操作员**  
显示当前所选操作员的“属性”对话框。 可以在“操作员属性”对话框上查看和修改操作员属性。  
  
## <a name="see-also"></a>另请参阅  
[警报](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[警报](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
  

