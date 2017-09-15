---
title: "实体同步关系 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 9abf874d3e813639f16e36b1ccc92cf178996f3a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="entity-sync-relationship-master-data-services"></a>实体同步关系 (Master Data Services)
  实体同步是实体版本间的单向可重复同步。 它使你可在不同模型间共享实体数据。 你可以在一个模型中保留单个事实源，并在其他模型中重用该主数据。 例如，你可以将 US 状态数据存储在一个模型实体中，并在其他模型中重用该数据。  
  
 使用实体同步，还可以制作数据的一次性副本。  
  
 在同步执行期间，源实体中所有具有自由格式和文件属性的叶成员都同步到目标实体。 这将创建、删除和修改实体架构和成员。  
  
 一旦建立了同步关系，则目标实体只能通过同步进程修改。 可以随时删除同步关系以使目标实体可编辑。  
  
## <a name="see-also"></a>另请参阅  
 [创建和执行实体同步关系 (Master Data Services)](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [编辑和删除实体同步关系 (Master Data Services)](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
