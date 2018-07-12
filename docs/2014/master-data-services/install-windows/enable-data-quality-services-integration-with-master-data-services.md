---
title: 实现 Data Quality Services 与 Master Data Services 的集成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
caps.latest.revision: 4
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 276b17d6e62f9ba45a02d1e3e325a457ff6ee77c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37164818"
---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>实现 Data Quality Services 与 Master Data Services 的集成
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，匹配功能由 Data Quality Services (DQS) 提供。 此功能必须启用后才能使用。  
  
## <a name="prerequisites"></a>必要條件  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 应用程序和数据库必须存在。  
  
-   Data Quality Services 功能和数据质量客户端必须安装在承载 MDS 数据库的同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上。 有关详细信息，请参阅 [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
### <a name="to-enable-data-quality-services-integration"></a>启用 Data Quality Services 集成  
  
1.  打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  在左窗格中单击 **“Web 配置”**。  
  
3.  在 **“Web 配置”** 页上，选择网站和 Web 应用程序。  
  
4.  在 **“启用 DQS 集成”** 部分中，单击 **“启用与 Data Quality Services 的集成”**。  
  
5.  在确认对话框中，单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [数据质量匹配中的 MDS 外接程序 excel](../microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [用于 Microsoft Excel 的 Master Data Services 外接程序](../microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [安装 Master Data Services](install-master-data-services.md)  
  
  
