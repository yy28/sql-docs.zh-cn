---
title: 将项目添加到和从发布 (SQL Server Management Studio) 中删除文章 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ea3c32da50b3ec5e2a2eb3d3bf58fad1e0323f10
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017519"
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
  
  