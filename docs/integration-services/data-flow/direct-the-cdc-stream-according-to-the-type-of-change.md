---
title: "定向 CDC 流根据更改类型 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3afa531e-f425-40a4-a1bf-1c3e1727287e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c520920a94c6c53a577953b313837aee0f7d584
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="direct-the-cdc-stream-according-to-the-type-of-change"></a>根据更改的类型定向 CDC 流
  若要添加并配置 CDC 拆分器转换，包必须包含至少一个数据流任务和一个 CDC 源。  
  
 添加到包的 CDC 源必须选择了 NetCDC 处理模式。 有关选择处理模式的详细信息，请参阅 [CDC 源编辑器（“连接管理器”页）](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)。  
  
### <a name="to-direct-the-cdc-stream-according-to-the-type-of-change"></a>根据更改的类型定向 CDC 流  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含所需包的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”**把 CDC 拆分器拖动到设计图面。  
  
4.  将在包中包含的 CDC 源连接到 CDC 拆分器。  
  
5.  将 CDC 拆分器连接到一个或多个目标。 您可以连接最多三个不同的输出。  
  
6.  选择以下输出之一：  
  
    -   删除输出：定向 DELETE 更改行的输出。  
  
    -   插入输出：定向 INSERT 更改行的输出。  
  
    -   更新输出：之前/之后 UPDATE 更改行和 Merge 更改行定向的输出。  
  
7.  或者，您可以使用 **“高级编辑器”** 对话框配置高级属性。  
  
     **“高级编辑器”** 对话框包含可通过编程方式设置的属性。  
  
     打开 **“高级编辑器”** 对话框：  
  
    -   在您的 **项目的** “数据流” [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 屏幕上，右键单击 CDC 拆分器，然后选择 **“显示高级编辑器”**。  
  
     有关使用 CDC 拆分器的详细信息，请参阅 Microsoft SQL Server Integration Services 的 CDC 组件。  
  
## <a name="see-also"></a>另请参阅  
 [CDC 拆分器](../../integration-services/data-flow/cdc-splitter.md)  
  
  

