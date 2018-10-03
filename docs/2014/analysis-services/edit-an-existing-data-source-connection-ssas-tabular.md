---
title: 编辑现有的数据源连接 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.selexistconn.f1
ms.assetid: 97e63f18-a01d-4c91-a411-e7e6d40a0647
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a177971e13a100044ccc40de44b93dbf6816478
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117797"
---
# <a name="edit-an-existing-data-source-connection-ssas-tabular"></a>编辑现有数据源连接（SSAS 表格）
  本主题介绍如何编辑表格模型中现有数据源连接的属性。  
  
 在创建与外部数据源的连接后，可以通过以下方式修改该连接：  
  
-   可以更改连接信息，其中包括：用作源的文件、馈送或数据库，其属性或其他特定于访问接口的连接选项。  
  
-   可以更改表和列映射，删除不再使用的列引用。  
  
-   可以更改从外部数据源获取的表、视图或列。  
  
## <a name="modify-a-connection"></a>修改连接  
 此过程介绍如何修改数据库的数据源连接。 使用数据源的某些选项将根据数据源类型而有所不同；但是，您应该能够轻松地标识这些差异。  
  
#### <a name="to-change-the-external-data-source-used-by-a-current-connection"></a>更改当前连接使用的外部数据源  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“现有连接”**。  
  
2.  选择您要修改的数据源连接，然后单击 **“编辑”**。  
  
3.  在 **“编辑连接”** 对话框中，单击 **“浏览”** 找到类型相同但名称或位置不同的其他数据库。  
  
     更改数据库文件后，将立即显示一条消息，指示您需要保存和刷新表以便查看新数据。  
  
4.  单击 **“保存”**，然后单击 **“关闭”**。  
  
5.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，依次单击 **“模型”**、 **“处理”** 和 **“全部处理”**。  
  
     将使用新数据源重新处理表，但保留原有的数据选择。  
  
    > [!NOTE]  
    >  如果新数据源包含原始数据源中不存在的任何附加表，您必须重新打开已更改的连接并添加这些表。  
  
## <a name="edit-table-and-column-mappings-bindings"></a>编辑表和列映射（绑定）  
 此过程说明如何在更改数据源之后编辑映射。  
  
#### <a name="to-edit-column-mappings-when-a-data-source-changes"></a>在数据源发生更改时编辑列映射  
  
1.  在模型设计器中，选择某个表。  
  
2.  单击 **“表”** 菜单，然后单击 **“表属性”**。  
  
     **“表名”** 框中将显示所选表的名称。 **“源名称”** 框包含外部数据源中的表的名称。 如果源和模型中对列的命名方式不同，则可通过选择 **“源”** 或 **“模型”** 选项在这两组列名之间进行切换。  
  
3.  若要更改用作数据源的表，请为 **“源名称”** 选择当前表之外的其他表。  
  
4.  在需要时更改列映射：  
  
    1.  若要添加源中存在但模型中不存在的列，请选中列名旁边的复选框。  
  
         实际数据将在下次进行刷新时加载到模型中。  
  
    2.  如果模型中有些列在当前数据源中不再可用，将在通知区域显示一条消息，其中列出无效的列。 您无需执行任何其他操作。  
  
5.  单击 **“保存”** 将更改应用于源。  
  
     在您保存当前的一组表属性时，可能会显示一条消息，指示您需要处理表。 单击 **“处理”** 可将更新的数据加载到模型中。  
  
## <a name="see-also"></a>请参阅  
 [处理数据&#40;SSAS 表格&#41;](process-data-ssas-tabular.md)   
 [支持的数据源（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
