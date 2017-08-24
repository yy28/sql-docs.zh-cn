---
title: "将查询参数映射到数据流组件中的变量 |Microsoft 文档"
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
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: da9367a56cefbb37244d4a47543b93586e7e8870
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>将查询参数映射到数据流组件中的变量
  当配置 OLE DB 源以使用参数化查询时，可以将参数映射到变量。  
  
 当 OLE DB 源连接到数据源时，OLE DB 源使用参数化查询来筛选数据。  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>将查询参数映射到变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”**中将 OLE DB 源拖动到设计图面。  
  
4.  右键单击 OLE DB 源，再单击“编辑”。  
  
5.  在 **“OLE DB 源编辑器”**中，选择用于连接到数据源的 OLE DB 连接管理器，或单击 **“新建”** 以创建一个新的 OLE DB 连接管理器。  
  
6.  对于数据访问模式，请选择 **“SQL 命令”** 选项，然后在 **“SQL 命令文本”** 窗格中键入参数化查询。  
  
7.  单击 **“参数”**。  
  
8.  在**设置查询参数**对话框框中，映射中的每个参数**参数**到中的变量的列表**变量**列表，或通过单击创建新变量**\<新变量 >**。 单击 **“确定”**。  
  
    > [!NOTE]  
    >  只有在包作用域内的系统变量和用户定义变量，诸如 Foreach 循环容器这样的父容器或者包含数据流组件的数据流任务，才用于映射。 变量的数据类型必须与参数所分配的 WHERE 子句的列兼容。  
  
9. 单击 **“预览”** 以查看查询返回的数据（最多 200 行）。  
  
10. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 源](../../integration-services/data-flow/ole-db-source.md)   
 [查找转换](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
