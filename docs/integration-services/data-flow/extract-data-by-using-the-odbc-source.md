---
title: 使用 ODBC 源提取数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: efc8ce0a541a508f88e7b1122b561008e25f4d51
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292672"
---
# <a name="extract-data-by-using-the-odbc-source"></a>使用 ODBC 源提取数据

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  本过程说明如何通过使用 ODBC 源来提取数据。 若要添加和配置 ODBC 源，包中必须已经包含至少一个数据流任务。  
  
### <a name="to-extract-data-using-an-odbc-source"></a>使用 ODBC 源提取数据  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开所需的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
2.  单击 **“数据流”** 选项卡，然后从 **“工具箱”** 把 ODBC 源拖动到设计图面。  
  
3.  双击此 ODBC 源。  
  
4.  在 **“ODBC 源编辑器”** 对话框中的 **“连接管理器”** 页上，选择现有的 ODBC 连接管理器，或单击 **“新建”** 创建新的连接管理器。  
  
5.  选择数据访问方法。  
  
    -   **表名**：在数据库中选择某个表或视图，或者键入一个正则表达式以便标识 ODBC 连接管理器连接到的表。  
  
         该列表仅包含前 1000 个表。 如果您的数据库包含超过 1000 个表，则可以键入表名的开头，或者使用 (*) 通配符输入名称的任何部分以便显示要使用的表。  
  
    -   **SQL 命令**：键入 SQL 命令，或单击“浏览”  从文本文件中加载 SQL 查询。  
  
6.  可以单击 **“预览”** ，查看最多 200 行 ODBC 源所提取的数据。  
  
7.  若要更新外部列和输出列之间的映射，请单击 **“列”** ，并在 **“外部列”** 列表中选择其他列。  
  
8.  如果需要，可以通过编辑 **“输出列”** 列表中的值来更新输出列的名称。  
  
9. 若要配置错误输出，请单击 **“错误输出”** 。  
  
10. 单击“确定”  。  
  
11. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 源编辑器（“连接管理器”页）](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [ODBC 源编辑器（“列”页）](../../integration-services/data-flow/odbc-source-editor-columns-page.md)   
 [ODBC 源编辑器（“错误输出”页）](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  
