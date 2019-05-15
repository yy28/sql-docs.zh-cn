---
title: 删除对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.deleteobjects.f1
helpviewer_keywords:
- Delete Objects dialog box
ms.assetid: 49541441-179c-40d3-ba0c-01bcae545984
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 35ce645577ca276f4f5ec6a5792d27859369a821
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102758"
---
# <a name="delete-objects"></a>删除对象
  使用此对话框可以删除数据库或数据库对象。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **要删除的对象**  
 显示要删除的对象的名称、类型、所有者和状态，以及在执行过程中的所有错误消息。  
  
> [!NOTE]  
>  对数据库运行“删除”与在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中发出 DROP DATABASE 等效。  
  
 **显示依赖关系**  
 单击此项可显示依赖于当前所选对象的对象，以及当前对象所依赖的对象（向上和向下依赖关系）。 “显示依赖关系”对话框中显示的信息是只读的。  
  
> [!NOTE]  
>  并不是所有类型的数据库对象都会出现“显示依赖关系”按钮。 若要在“显示依赖关系”按钮不可用时查看依赖关系，请在对象资源管理器中右键单击该对象，再单击“查看依赖关系”。  
  
 **删除数据库备份和还原历史记录信息**  
 只在删除数据库时出现，此复选框会导致从 **msdb** 数据库中删除主题数据库的备份和还原历史记录。  
  
 **关闭现有连接**  
 只在删除数据库时出现，此复选框可以终止与主题数据库的连接。  
  
  
