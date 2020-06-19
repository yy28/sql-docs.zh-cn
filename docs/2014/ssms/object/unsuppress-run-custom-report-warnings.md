---
title: 启用运行自定义报表警告 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: stevestein
ms.author: sstein
ms.openlocfilehash: ae7f4d08ac613113d715728a5cb78ae37bd6f99b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058527"
---
# <a name="unsuppress-run-custom-report-warnings"></a>启用运行自定义报表警告
  对于自定义报表，有两个警告对话框。 本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中取消显示这些对话框。  
  
 默认情况下，在运行自定义报表之前会显示“运行自定义报表”  对话框。 如果选中“请不要再显示此警告”  复选框，将不再显示此对话框。 此外，在默认情况下，如果打开一个自定义报表然后单击链接打开另外一个自定义报表，则也将显示此“运行自定义报表”  对话框。 此对话框显示钻取自定义报表文件的填写路径。 如果选中“请不要再显示此警告”  复选框，将不再显示此对话框。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>启用主自定义报表警告对话框  
  
1.  连接到 \<*Server*> \\ < *Share* >| \<*Drive*> \Documents and Settings \\<UserProfile \> \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml。  
  
2.  右键单击 `reports.xml` ，然后单击 "**编辑**"。  
  
3.  将** \<SuppressWarning> true \</SuppressWarning> 更改 \<SuppressWarning> 为 \</SuppressWarning> false**。  
  
4.  重新启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>启用钻取自定义报表警告对话框  
  
1.  连接到 \<*Server*> \\ < *Share* >| \<*Drive*> \Documents and Settings \\<UserProfile \> \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml。  
  
2.  右键单击 `reports.xml` ，然后单击 "**编辑**"。  
  
3.  将** \<SuppressDrillthroughWarning> true \</SuppressDrillthroughWarning> 更改 \<SuppressDrillthroughWarning> 为 \</SuppressDrillthroughWarning> false**。  
  
4.  重新启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio 中的自定义报表](custom-reports-in-management-studio.md)   
 [将自定义报表添加到 Management Studio](add-a-custom-report-to-management-studio.md)   
 [将自定义报告与对象资源管理器节点属性一起使用](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
