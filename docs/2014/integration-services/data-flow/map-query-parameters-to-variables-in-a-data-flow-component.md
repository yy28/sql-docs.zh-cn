---
title: 将查询参数映射到数据流组件中的变量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8a02dbe6174af6dbfefb472b7dddfb878fb569d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228767"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>将查询参数映射到数据流组件中的变量
  当配置 OLE DB 源以使用参数化查询时，可以将参数映射到变量。  
  
 当 OLE DB 源连接到数据源时，OLE DB 源使用参数化查询来筛选数据。  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>将查询参数映射到变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”** 中将 OLE DB 源拖动到设计图面。  
  
4.  右键单击 OLE DB 源，再单击“编辑”。  
  
5.  在 **“OLE DB 源编辑器”** 中，选择用于连接到数据源的 OLE DB 连接管理器，或单击 **“新建”** 以创建一个新的 OLE DB 连接管理器。  
  
6.  对于数据访问模式，请选择 **“SQL 命令”** 选项，然后在 **“SQL 命令文本”** 窗格中键入参数化查询。  
  
7.  单击 **“参数”**。  
  
8.  在“设置查询参数”对话框中，将“参数”列表中的每个参数映射到“变量”列表中的某个变量，或通过单击“\<新建变量>”创建新的变量。 单击“确定” 。  
  
    > [!NOTE]  
    >  只有在包作用域内的系统变量和用户定义变量，诸如 Foreach 循环容器这样的父容器或者包含数据流组件的数据流任务，才用于映射。 变量的数据类型必须与参数所分配的 WHERE 子句的列兼容。  
  
9. 单击 **“预览”** 以查看查询返回的数据（最多 200 行）。  
  
10. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 源](ole-db-source.md)   
 [查找转换](transformations/lookup-transformation.md)  
  
  
