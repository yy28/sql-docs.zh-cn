---
title: 删除版本 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29a4c0bb160a291dc4fd5d015f676f1d3c84b2f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478603"
---
# <a name="delete-a-version-master-data-services"></a>删除版本 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您确定您不再需要与某个版本关联的主数据时，可以删除此版本。 删除版本后，无法检索关联的主数据。  
  
> [!WARNING]  
>  如果模型只有一个版本而您删除它，则模型将变得不可用。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须具有查看 mdm.viw_SYSTEM_SCHEMA_VERSION 视图的权限和在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中执行 mds.udpVersionDelete 存储过程的权限。 有关详细信息，请参阅[数据库对象安全性 (Master Data Services)](../master-data-services/database-object-security-master-data-services.md)。  
  
### <a name="to-delete-a-version"></a>删除版本  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例。  
  
2.  打开 mdm.viw_SYSTEM_SCHEMA_VERSION 视图。  
  
3.  找到您要删除的模型的版本，并复制 **ID** 字段中的值。  
  
4.  创建新查询。  
  
5.  键入以下文本，用在步骤 2 中复制的值替代 *version_ID* 。  
  
    ```  
    EXEC [mdm].[udpVersionDelete] @Version_ID='version_ID'  
    ```  
  
6.  运行查询。  
  
    > [!NOTE]  
    >  您可能必须等待几分钟，然后 Web 应用程序才能反映此更改。  
  
## <a name="see-also"></a>请参阅  
 [版本 (Master Data Services)](../master-data-services/versions-master-data-services.md)   
 [复制版本 (Master Data Services)](../master-data-services/copy-a-version-master-data-services.md)  
  
  
