---
title: "教程： 使用 OData 源 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: cbdc4a2e0719e65e378d232c5abcb5404e8342f1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/23/2017

---
# <a name="tutorial-using-the-odata-source"></a>教程：使用 OData 源
  本教程介绍了从示例 **Northwind** OData 服务 (http://services.odata.org/V3/Northwind/Northwind.svc/) 提取 **Employees** 集合，然后将它加载到某一平面文件中的过程。  
  
## <a name="1-create-an-integration-services-project"></a>1.创建 Integration Services 项目  
  
1.  启动 **SQL Server Data Tools** 或 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
2.  单击 **“文件”**，指向 **“新建”**，然后单击 **“项目”**。  
  
3.  在“新建项目”对话框中，依次展开“已安装”、“模板”“商业智能”，然后单击“Integration Services”。  
  
4.  对于项目类型，选择 **“Integration Services 项目”** 。  
  
5.  为项目输入 **“名称”** 并且选择 **“位置”** ，然后单击 **“确定”**。  
  
## <a name="2-add-and-configure-an-odata-source"></a>2.添加和配置 OData 源 
  
1.  将“数据流任务”从“SSIS 工具箱”拖放到 SSIS 包的控制流设计图面上。  
  
2.  单击**数据流**选项卡上，或双击**数据流任务**以打开数据流设计图面。  
  
3.  从“SSIS 工具箱”的“公共”组中拖放“OData 源”。
  
4.  双击**OData 源**组件可启动**OData 源编辑器**对话框。  
  
5.  单击 **“新建…”** 可添加新的 OData 连接管理器。  
  
6.  为 **“服务文档位置”**输入 OData 服务 URL。 此 URL 可以是指向服务文档，或特定馈送或实体的 URL。 就本教程来说，输入的服务文档的 URL: [http://services.odata.org/V3/Northwind/Northwind.svc/](http://services.odata.org/V3/Northwind/Northwind.svc/)。  
  
7.  确认为 **“身份验证”** 选择了 **“Windows 身份验证”** ，以便用于访问 OData 服务。 默认情况下将选择**“Windows 身份验证”** 。  
  
8.  单击**测试连接**以测试该连接，并单击**确定**以完成创建 OData 连接管理器的实例。  
  
9. 在 **“OData 源编辑器”** 对话框中，确认为 **“对资源路径使用集合”** 选项选择了 **“集合”** 。  
  
10. 从**集合**下拉列表中，选择**员工**。  
  
11. 为 **“查询选项”**输入任何其他 OData 查询选项或筛选器。 例如， `$orderby=CompanyName&$top=100`。 就本教程来说，输入`$top=5`。  
  
12. 单击 **“预览”** 可预览数据。  
  
13. 在左导航窗格中单击 **“列”** 可切换到 **“列”** 页。  
  
14. 通过选中相应复选框，从 **“可用外部列”**中选择 **EmployeeID**、 **FirstName** 和 **LastName** 。  
  
15. 单击 **“确定”** 关闭 **“OData 源编辑器”** 对话框。  
  
## <a name="3-add-and-configure-a-flat-file-destination"></a>3.添加和配置平面文件目标
  
1.  现在，将“平面文件目标”从“SSIS 工具箱”拖放到“OData 源”组件下的数据流设计图面上。  
  
2.  使用蓝色箭头将 **“OData 源”** 组件与 **“平面文件目标”** 组件连接起来。  
  
3.  双击“平面文件目标”。 您应该会看到 **“平面文件目标编辑器”** 对话框。  
  
4.  在 **“平面文件目标编辑器”** 对话框中，单击 **“新建”** 创建新的平面文件连接管理器。  
  
5.  在 **“平面文件格式”** 对话框中，选择 **“带分隔符”**。 然后你会看到**平面文件连接管理器编辑器**对话框。  
  
6.  在**平面文件连接管理器编辑器**对话框中，为**文件名**，输入`c:\Employees.txt`。  
  
7.  在左侧导航窗格中，单击 **“列”**。 您可以预览此页上的数据。  
  
8.  单击“确定”关闭 **“平面文件连接管理器编辑器”** 对话框。  
  
9. 在 **“平面文件目标编辑器”** 对话框中，在左侧导航窗格中单击 **“映射”** 。 查看映射。  
  
10. 单击“确定” **关闭“平面文件目标编辑器”** 对话框。  

## <a name="4-run-the-package"></a>4.运行包
运行 SSIS 包。 验证输出文件创建使用 ID、 名字和姓氏的五个员工从 OData 源。
  
  

