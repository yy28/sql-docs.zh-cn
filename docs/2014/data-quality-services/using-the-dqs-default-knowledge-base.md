---
title: 使用 DQS 默认知识库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d0fa10fa26f46857bd4f6848bd98bdcf1d65253a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484077"
---
# <a name="using-the-dqs-default-knowledge-base"></a>使用 DQS 默认知识库
  本主题介绍随 **(DQS) 一起安装的默认知识库**DQS 数据 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 。 这是包含以下域的预先生成的默认知识库：  
  
-   **国家/地区**：包含常规长名称（国家/地区指定的官方名称）和短名称（列表、地图等中使用的通用名称）、两字母缩写形式、三字母缩写形式和三位代码。  将前导值设置为国家/地区长名称。  
  
-   **国家/地区（三字母前导）**：包含常规长名称（国家/地区指定的官方名称）和短名称（列表、地图等中使用的通用名称）、两字母缩写形式、三字母缩写形式和三位代码。  将前导值设置为国家/地区三字母缩写形式。  
  
-   **国家/地区（两字母前导）**：包含常规长名称（国家/地区指定的官方名称）和短名称（列表、地图等中使用的通用名称）、两字母缩写形式、三字母缩写形式和三位代码。  将前导值设置为国家/地区两字母缩写形式。  
  
-   **美国-县**：包含美国县的列表。  
  
-   **US**姓：包含在人口普查2000中出现100或更多次的姓氏（姓氏）的列表。  
  
-   **US**：包含50州、哥伦比亚特区和从人口普查2010中提取的波多黎各的位置列表。  
  
-   **美国-州**：包含美国每个州的常规长（官方）名称和两字母缩写形式。 将前导值设置为常规州名称。  
  
-   **美国-州（2-字母标题）**：包含美国每个州的常规长（官方）名称和两字母缩写形式。 将前导值设置为两字母缩写形式的州名称。  
  
## <a name="using-the-default-knowledge-base"></a>使用默认知识库  
 您可以通过以下方式使用默认 DQS 知识库（DQS 数据）。  
  
-   使用默认知识库快速启动并运行清理数据质量项目，而不必首先在 DQS 中创建新知识库。  
  
-   对默认知识库运行“域管理”、“知识发现”或“匹配策略”活动。 为此，请单击 **Data Quality Client Home Screen** 中的 [“打开知识库”](../../2014/data-quality-services/data-quality-client-home-screen.md)，在 **“打开知识库”** 屏幕中选择 **“DQS 数据”** 知识库，然后在 **“选择活动”** 区域中选择所需的活动。 单击“下一步”继续。   
  
-   使用默认知识库创建新知识库。 要从现有知识库创建知识库，请参阅 [Create a Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md)。  
  
-   在 [Integration Services 中的 DQS 清理组件](https://go.microsoft.com/fwlink/?LinkId=238830) 和 [Master Data Services Excel 外接程序](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)中使用它。  
  
## <a name="see-also"></a>另请参阅  
 [DQS 知识库和域](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
