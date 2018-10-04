---
title: 导入 Integration Services 项目 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 3301c328-b0f5-4517-915c-93713413e453
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f81996093aa6ac42eaab9c6057c9c8bb706055b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203797"
---
# <a name="import-an-integration-services-project"></a>导入 Integration Services 项目
  使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的“导入项目向导”可以根据现有的部署文件 (.ispac) 或部署到 Integration Services 目录的项目创建一个项目。 如果您没有项目的原始副本，但又想根据 .ispac 文件或 SSISDB 目录创建一个项目，此时该功能特别有用。  
  
### <a name="to-import-a-project"></a>导入项目  
  
1.  在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的“文件”菜单上，单击“新建” > “项目”。  
  
2.  在 **“新建项目”** 窗口的 **“已安装的模板”** 区域中，展开 **“商业智能”**，然后单击 **“Integration Services”**。  
  
3.  从项目类型列表中选择 **“Integration Services 导入项目向导”** 。  
  
4.  在 **“名称”** 文本框中为即将创建的新项目键入名称。  
  
5.  在 **“位置”** 文本框中键入项目的路径或位置，或者单击 **“浏览”** 选择一个位置。  
  
6.  在 **“解决方案名称”** 文本框中键入解决方案的名称。  
  
7.  单击 **“确定”** 启动 **“Integration Services 导入项目向导”** 对话框。  
  
8.  单击 **“下一步”** 切换到 **“选择源”** 页。  
  
9. 如果要从 **.ispac** 文件导入，请在 **“路径”** 文本框中键入包含文件名的路径。 单击 **“浏览”** 导航到要存储解决方案的文件夹，在 **“文件名”** 文本框中键入文件名，然后单击 **“打开”**。  
  
     如果要从 **“Integration Services 目录”** 导入，请在 **“服务器名称”** 文本框中键入数据库实例名称，或者单击 **“浏览”** 选择包含该目录的数据库实例。  
  
     单击 **“路径”** 文本框旁边的 **“浏览”** ，展开目录中的文件夹，选择要导入的项目，然后单击 **“确定”**。  
  
     单击 **“下一步”** 切换到 **“查看”** 页。  
  
10. 查看信息，然后单击 **“导入”** 以基于您所选的现有项目创建一个项目。  
  
11. 可选：单击 **“保存报表”** 将结果保存到文件中。  
  
12. 单击 **“关闭”** 以关闭 **“Integration Services 导入项目向导”** 对话框。  
  
  
