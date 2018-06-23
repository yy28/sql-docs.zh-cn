---
title: 验证 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 769e3e1cba3179ab9a3040094f1d88f79c3c6d55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128570"
---
# <a name="validation-master-data-services"></a>验证 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，对数据进行验证以确保其准确性。 一些验证自动发生，而另一些验证则基于管理员创建的业务规则。  
  
## <a name="when-data-validation-occurs"></a>何时发生数据验证  
 验证发生在不同的时间，并以不同的方式显示在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 应用程序中。  
  
|验证类型|标准确定者|发生条件|在 MasterData 管理器 Web UI 中显示为|在 Excel 外接程序中显示为|是否将数据保存到 MDS 存储库？|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|业务规则验证|MDS 管理员|当用户添加或编辑数据时自动发生。<br /><br /> 当用户应用业务规则时手动发生。<br /><br /> 当管理员在 **Web 应用程序的** “版本管理” [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 功能区域中验证某版本是否符合业务规则时手动发生。|验证错误|ValidationStatus|是|  
|数据类型和内容验证|MDS 管理员，当创建模型对象（例如，属性的长度或数据类型）时|当用户添加或编辑数据时自动发生|输入错误|InputStatus|“否”|  
|数据类型和内容验证|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|当用户添加或编辑数据时自动发生|输入错误|InputStatus|“否”|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|创建业务规则并发布它们，以便针对它们验证数据。|[创建和发布业务规则&#40;Master Data Services&#41;](create-and-publish-a-business-rule-master-data-services.md)|  
|根据业务规则验证数据版本。 仅限于管理员。|[针对业务规则验证版本&#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|根据业务规则验证数据的特定子集。 有权访问 **“资源管理器”** 功能区域的所有用户。|[针对业务规则验证特定成员&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|根据业务规则验证数据的特定子集。 有权访问 **“资源管理器”** 功能区域且使用 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]的所有用户。|[应用业务规则&#40;MDS add-in for Excel&#41;](microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>请参阅  
 [业务规则&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  