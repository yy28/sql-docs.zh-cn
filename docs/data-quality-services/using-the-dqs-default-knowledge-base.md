---
title: "使用 DQS 默认知识库 | Microsoft Docs"
ms.custom: ""
ms.date: "07/31/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# 使用 DQS 默认知识库
  本主题介绍了默认知识库， **DQS 数据**, ，与安装的哪些 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)。 这是包含以下域的预先生成的默认知识库：  
  
-   **国家/地区**︰ 包含常规长 （国家/地区指定的官方名称） 和短名称 （列表、 地图等中使用的通用名称）、 两字母缩写形式、 三字母缩写形式和三位数字代码，为每个位置。  将前导值设置为国家/地区长名称。  
  
-   **国家/地区 （三字母前导）**︰ 包含常规长 （国家/地区指定的官方名称） 和短名称 （列表、 地图等中使用的通用名称）、 两字母缩写形式、 三字母缩写形式和三位数字代码，为每个位置。  将前导值设置为国家/地区三字母缩写形式。  
  
-   **国家/地区 （两字母前导）**︰ 包含常规长 （国家/地区指定的官方名称） 和短名称 （列表、 地图等中使用的通用名称）、 两字母缩写形式、 三字母缩写形式和三位数字代码，为每个位置。  将前导值设置为国家/地区两字母缩写形式。  
  
-   **美国-县**︰ 包含美国县的列表。  
  
-   **美国-姓氏**︰ 包含列表的最后一个名称 （姓） 出现 100 或更多次在 2000 年人口普查中。  
  
-   **美国-地方**︰ 包含 50 个州、 哥伦比亚特区和波多黎各从美国人口普查 2010年中提取的位置的列表。  
  
-   **美国-州**︰ 包含常规长 （官方） 名称和美国各州的两个字母缩写形式。 将前导值设置为常规州名称。  
  
-   **美国-州 （两个字母标题）**︰ 包含常规长 （官方） 名称和美国各州的两个字母缩写形式。 将前导值设置为两字母缩写形式的州名称。  
  
## 使用默认知识库  
 您可以通过以下方式使用默认 DQS 知识库（DQS 数据）。  
  
-   使用默认知识库快速启动并运行清理数据质量项目，而不必首先在 DQS 中创建新知识库。  
  
-   对默认知识库运行“域管理”、“知识发现”或“匹配策略”活动。 为此，请单击 **Data Quality Client Home Screen** 中的 [“打开知识库”](../data-quality-services/data-quality-client-home-screen.md)，在 **“打开知识库”** 屏幕中选择 **“DQS 数据”** 知识库，然后在 **“选择活动”** 区域中选择所需的活动。 单击 **“下一步”** 继续。  
  
-   使用默认知识库创建新知识库。 要从现有知识库创建知识库，请参阅 [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md)。  
  
-   将其用于 [Integration Services 中的 DQS 清理组件](http://go.microsoft.com/fwlink/?LinkId=238830) 和 [Master Data Services 外接程序 excel](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)。  
  
## 另请参阅  
 [DQS 知识库和域](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  