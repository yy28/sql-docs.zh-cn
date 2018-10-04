---
title: 添加和删除项目从发布 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b41b9c0d37437e3faeec733ff3ce390dc4ae15a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056637"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication-sql-server-management-studio"></a>将项目添加到发布中以及从发布中删除项目 (SQL Server Management Studio)
  在新建发布向导中创建项目时，首次将其添加到发布中。 有关使用此向导的详细信息，请参阅[创建发布](create-a-publication.md)。  
  
 创建发布后，在“发布属性 - \<发布>”对话框的“项目”页上添加和删除项目。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](view-and-modify-publication-properties.md)。 有关添加和删除项目的注意事项的信息，请参阅[向现有发布添加项目和从中删除项目](add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>创建发布后添加项目  
  
1.  在“发布属性 - \<发布>”对话框的“项目”页上，取消选中“仅在列表中显示已选中的对象”复选框。 这样可以查看发布数据库中未发布的对象。  
  
2.  选中要添加的每个项目旁边的复选框。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>删除项目  
  
1.  在“发布属性 - \<发布>”对话框的“项目”页上，取消选中要删除的每个项目旁边的复选框。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [定义项目](define-an-article.md)   
 [发布数据和数据库对象](publish-data-and-database-objects.md)  
  
  
