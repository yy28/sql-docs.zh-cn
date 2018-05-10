---
title: 通过使用 ODBC 目标来加载数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5875b2783e02a022f027f1352d6f6621c2754182
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="load-data-by-using-the-odbc-destination"></a>通过使用 ODBC 目标来加载数据
  本过程说明如何使用 ODBC 目标加载数据。 若要添加和配置 ODBC 目标，包中必须已包含至少一个数据流任务和源。  
  
### <a name="to-load-data-using-an-odbc-destination"></a>使用 ODBC 目标加载数据  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  单击 **“数据流”** 选项卡，再将 ODBC 目标从 **“工具箱”**拖动到设计图面。  
  
3.  将数据流组件的可用输出拖到 ODBC 目标的输入。  
  
4.  双击此 ODBC 目标。  
  
5.  在 **“ODBC 目标编辑器”** 对话框中的 **“连接管理器”** 页上，选择现有的 ODBC 连接管理器，或单击 **“新建”** 创建新的连接管理器。  
  
6.  选择数据访问方法。  
  
    -   **表名 - 批处理**：选择此选项可将 ODBC 目标配置为在批处理模式下工作。 当您选择此选项时，可以设置 **“批处理大小”**。  
  
    -   **表名 - 逐行**：选择此选项可以将 ODBC 目标配置为一次一行将各行插入目标表中。 选择此选项时，数据将一次一行加载到表中。  
  
7.  在 **“表或视图的名称”** 字段中，从列表的数据库中选择某一可用表或视图，或者键入正则表达式以便标识表。该列表仅包含前 1000 个表。 如果您的数据库包含超过 1000 个表，则可以键入表名的开头，或者使用 (*) 通配符输入名称的任何部分以便显示要使用的表。  
  
8.  可以单击 **“预览”** ，查看在 ODBC 目标中选择的表中的最多 200 行数据。  
  
9. 单击 **“映射”** ，然后将列从一个列表拖动到另一个列表，从而将 **“可用输入列”** 列表中的列映射到 **“可用目标列”** 列表中的列。  
  
10. 若要配置错误输出，请单击 **“错误输出”**。  
  
11. 单击“确定” 。  
  
12. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 目标编辑器（“连接管理器”页）](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 目标编辑器（“映射”页）](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)   
 [ODBC 源编辑器（“错误输出”页）](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  
