---
title: 任务 4： 创建使用 SQL Server Data Tools SSIS 项目 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a6fb09370b01a88c23d75b843d588626ed96c9b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208067"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>任务 4：使用 SQL Server Data Tools 创建 SSIS 项目
  通过使用在此任务中，创建一个 SSIS 项目**SQL Server Data Tools**来自动执行清理和匹配供应商数据。  
  
1.  启动 **SQL Server Data Tools**。 单击开始，指向**所有程序**，展开**Microsoft SQL Server 2012**，然后单击**SQL Server Data Tools**。  
  
2.  在 **“文件”** 菜单中，指向 **“新建”**，然后单击 **“项目”**。  
  
3.  展开**商业智能**中**已安装的模板**窗格，然后选择**Integration Services**。  
  
     ![Visual Studio 的新建项目对话框](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio 的新建项目对话框")  
  
4.  选择**Integration Services 项目**中**项目类型列表**。  
  
5.  类型**CleanseAndCurateSuppliers**有关**名称**然后单击**确定**。  
  
6.  在中**解决方案资源管理器**窗口中，右键单击**Package.dtsx** ，然后选择**重命名**。 如果没有看到**解决方案资源管理器**窗口中，单击**视图**单击菜单栏上**解决方案资源管理器**。  
  
     ![Package.dtsx-重命名菜单](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package.dtsx-重命名菜单")  
  
7.  类型**CleanseAndCurate.dtsx**然后按**ENTER**。 请确保**扩展**保持 **.dtsx**。  
  
## <a name="next-step"></a>下一步  
 [任务 5：添加数据流任务](task-5-adding-data-flow-task.md)  
  
  
