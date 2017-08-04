---
title: "检索和了解变更数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],retrieving data
ms.assetid: af366697-6942-42bb-aea5-18fdef018965
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: caf66f974e832fcd1b27caf650d187942b3f19fe
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="retrieve-and-understand-the-change-data"></a>检索和了解变更数据
  在用于执行变更数据增量加载的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的数据流中，第一个任务是运行查询以检索变更数据。 在数据流任务中在源组件内执行此查询。 然后，使用下游转换和目标将变更数据应用到目标。  
  
> [!NOTE]  
>  在创建用于执行变更数据增量加载的包的过程中，第三步是创建包含表值函数的查询。 有关此查询的详细信息，请参阅[创建函数以检索变更数据](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)。 有关创建用于执行变更数据增量加载的包的完整过程的说明，请参阅[变更数据捕获 (SSIS)](../../integration-services/change-data-capture/change-data-capture-ssis.md)。  
  
## <a name="adding-the-data-flow-task"></a>添加数据流任务  
 在包的数据流中，您将检索变更数据，根据所发生的变更的类型分隔行，然后将变更应用到目标。  
  
#### <a name="to-add-a-data-flow-task-to-the-package"></a>向包添加数据流任务  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 **“控制流”** 选项卡上，添加数据流任务。  
  
2.  将准备查询字符串的前一任务连接到数据流任务。  
  
## <a name="configuring-the-source-component-to-query-for-changes"></a>配置源组件以查询变更  
 源组件使用已准备好并存储在变量中的查询字符串来调用用于检索已变更数据的表值函数。  
  
> [!NOTE]  
>  有关已准备好并存储在变量中的查询字符串的详细信息，请参阅 [准备查询变更数据](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)。 有关用于检索变更数据的表值函数的详细信息，请参阅 [创建函数以检索变更数据](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)。  
  
#### <a name="to-configure-an-ole-db-source-to-retrieve-the-change-data"></a>配置 OLE DB 源以检索变更数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 **“数据流”** 选项卡上，添加 OLE DB 源。  
  
2.  在 **“OLE DB 源编辑器”**的 **“连接管理器”** 页上，选择下列选项：  
  
    1.  配置到源数据库的有效连接。  
  
    2.  对于 **“数据访问模式”**，选择 **“变量中的 SQL 命令”**。  
  
    3.  对于 **“变量名称”**，选择 **“User::SqlDataQuery”**。  
  
3.  在 **“OLE DB 源编辑器”**中的 **“列”** 页上，确保所需的所有列都映射到输出列。  
  
## <a name="next-step"></a>下一步  
 在配置了用于检索变更数据的 OLE DB 源之后，下一步就是开始设计包中的数据流。  
  
 **下一个主题：**[处理插入、更新和删除](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)  
  
  
