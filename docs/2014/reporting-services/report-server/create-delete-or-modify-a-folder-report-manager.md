---
title: 创建、删除或修改文件夹（报表管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing folders
- modifying folders
- deleting folders
- folders [Reporting Services], creating
- folders [Reporting Services], deleting
- folders [Reporting Services], modifying
ms.assetid: d62159a8-ec67-4e28-a9f1-05a9250065bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef4aa341c8f89afbd099cd26fc8352425e6ac8ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103918"
---
# <a name="create-delete-or-modify-a-folder-report-manager"></a>创建、删除或修改文件夹（报表管理器）
  可以创建文件夹来组织和管理发布到报表服务器的项。 创建文件夹有助于用户查找他们关注的报表。 对于内容管理员来说，文件夹提供了应用权限的框架。 可以对特定的文件夹创建角色分配，来限制对处于开发阶段或者不应大范围分布的报表的访问。  
  
### <a name="to-create-a-folder"></a>创建文件夹  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器中，选择主文件夹，再单击 **“新建文件夹”**。 或者，若要在现有文件夹中创建文件夹，请在 **“内容”** 页中导航到该文件夹，再单击该文件夹将其打开。 然后单击 **“新建文件夹”**。  
  
     此时，将打开 **“新建文件夹”** 页。  
  
3.  键入文件夹名称。 文件夹名称可以包含空格，但不能包含以下用于 URL 编码的保留字符：; ? ： \@ & = +，$/* \< > |。 不能通过键入一系列文件夹名称来同时创建多个文件夹。  
  
4.  根据需要，可以键入说明。  
  
5.  如果不希望在 **“内容”** 页的默认视图中显示该文件夹，请选择 **“在列表视图中隐藏”** 。 只有在用户单击了 **“内容”** 页上的 **“显示详细信息”** 时，才可以看到该文件夹。  
  
6.  单击“确定”。   
  
### <a name="to-delete-a-folder"></a>删除文件夹  
  
1.  在报表管理器中，导航到 **“内容”** 页，然后找到要修改的项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击“删除”****。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-modify-or-delete-a-folder"></a>修改或删除文件夹  
  
1.  在报表管理器中，导航到 **“内容”** 页，然后找到要修改的项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”** 。 此时将打开“常规属性”页。  
  
4.  若要更改该文件夹位置，请单击 **“移动”**。 键入目标文件夹的位置，或从树中选择目标文件夹，再单击 **“确定”**。  
  
5.  或者，通过以下方式修改该文件夹属性：  
  
    -   若要修改关于该文件夹的显示文本，请键入名称或说明。  
  
    -   若要在 **“内容”** 页上的默认视图中显示该文件夹，请清除 **“在列表视图中隐藏”**。  
  
6.  或者，若要删除该文件夹及其内容，请单击 **“删除”**。  
  
7.  单击“应用”**** 保存所做的更改。  
  
## <a name="see-also"></a>另请参阅  
 [新文件夹页 &#40;报表管理器&#41;](../new-folder-page-report-manager.md)   
 ["内容" 页 &#40;报表管理器&#41;](../contents-page-report-manager.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
