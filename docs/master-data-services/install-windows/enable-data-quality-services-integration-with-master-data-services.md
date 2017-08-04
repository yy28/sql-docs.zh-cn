---
title: "启用 Data Quality Services 与 Master Data Services 的集成 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2086ab8ca26f813fe2e6c0a6ab3ec924f6024ab3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>实现 Data Quality Services 与 Master Data Services 的集成
  在[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，匹配功能提供 Data Quality Services (DQS)。 此功能必须启用后才能使用。  
  
## <a name="prerequisites"></a>先决条件  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 应用程序和数据库必须存在。  
  
-   Data Quality Services 功能和数据质量客户端必须安装在承载 MDS 数据库的同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上。 有关详细信息，请参阅 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
### <a name="to-enable-data-quality-services-integration"></a>启用 Data Quality Services 集成  
  
1.  打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  在左窗格中单击 **“Web 配置”**。  
  
3.  在 **“Web 配置”** 页上，选择网站和 Web 应用程序。  
  
4.  在 **“启用 DQS 集成”** 部分中，单击 **“启用与 Data Quality Services 的集成”**。  
  
5.  在确认对话框中，单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [数据质量匹配中的 MDS 外接 for Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Master Data Services 外接程序 Microsoft excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
