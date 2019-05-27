---
title: 参数化对话框的 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d60820ba7c384347aeeec80d8c41f934078eca8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056865"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  通过 **“参数化”** 对话框，可以将新参数或现有参数与某个任务的属性相关联。 可通过以下方式打开该对话框：在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中右键单击一个任务或“控制流”选项卡，然后单击“参数化”。 以下列表介绍了此对话框中的 UI 元素。 有关参数的详细信息，请参阅 [Integration Services (SSIS) 参数](integration-services-ssis-package-and-project-parameters.md)。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **属性**  
 选择要与参数相关联的任务属性。 此列表包含可参数化的所有属性。  
  
 **使用现有参数**  
 使用此选项可将任务属性与某个现有参数相关联，从而可以从下拉列表中选择该参数。  
  
 **不使用参数**  
 选择此选项可以删除对参数的引用。 不删除该参数。  
  
 **新建参数**  
 选择此选项可创建要与任务属性相关联的新参数。  
  
 **名称**  
 指定要创建的参数的名称。  
  
 **说明**  
 指定参数的说明。  
  
 **ReplTest1**  
 指定参数的默认值。 这也称作设计默认值，以后在部署时可以覆盖该值。  
  
 **范围**  
 通过选择“项目”或“包”选项指定参数的范围。 项目参数可用于向项目中的一个或多个包提供项目接收的任何外部输入。 利用包参数，您不必编辑和重新部署包就可以修改包执行。  
  
 **区分**  
 通过选中或清除该复选框，指定参数是否为敏感参数。 敏感参数值在目录中加密，并且在使用 Transact-SQL 或 SQL Server Management Studio 查看时以 NULL 值的形式出现。  
  
 **必需**  
 指定参数是否要求在执行包之前指定设计默认值之外的值。  
  
## <a name="uielement-list"></a>UIElement 列表  
  
