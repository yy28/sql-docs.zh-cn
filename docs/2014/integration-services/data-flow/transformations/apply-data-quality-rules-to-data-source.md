---
title: 将数据质量规则应用于数据源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c420a52528662cecec1bae8e0e1718152279bc0e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770453"
---
# <a name="apply-data-quality-rules-to-data-source"></a>将数据质量规则应用于数据源
  您可以使用 Data Quality Services (DQS) 来更正包数据流中的数据，方法是将 DQS 情理转换连接到数据源。 有关 DQS 的详细信息，请参阅 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)。 有关该转换的详细信息，请参阅 [DQS Cleansing Transformation](dqs-cleansing-transformation.md)。  
  
 使用 DQS 清理转换处理数据时，将在数据质量服务器上创建一个数据质量项目。 使用数据质量客户端管理项目。 有关详细信息，请参阅[管理（打开、解锁、重命名和删除）数据质量项目](../../../data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)。  
  
### <a name="to-correct-data-in-the-data-flow"></a>更正数据流中的数据  
  
1.  创建一个包。  
  
2.  添加并配置 DQS 清除转换。 有关详细信息，请参阅 [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md)。  
  
3.  将 DQS 清除转换连接到数据源。  
  
  
