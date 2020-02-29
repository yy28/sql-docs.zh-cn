---
title: 任务4：使用 SQL Server Data Tools 创建 SSIS 项目 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bcf16dc7d63e6a4acca6c30871666d1ffe996192
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171716"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>任务 4：使用 SQL Server Data Tools 创建 SSIS 项目
  在此任务中，你将通过使用**SQL Server Data Tools**来创建 SSIS 项目，以自动执行清理和匹配的供应商数据。

1.  启动**SQL Server Data Tools**。 单击 "开始"，指向 "**所有程序**"，展开**Microsoft SQL Server 2012**"，然后单击" **SQL Server Data Tools**"。

2.  在 **“文件”** 菜单中，指向 **“新建”**，然后单击 **“项目”**。

3.  在 "**已安装的模板**" 窗格中展开 "**商业智能**"，然后选择**Integration Services**。

     ![Visual Studio -“新建项目”对话框](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio -“新建项目”对话框")

4.  在**项目类型列表**中选择 " **Integration Services 项目**"。

5.  键入**CleanseAndCurateSuppliers**作为**名称**，然后单击 **"确定"**。

6.  在**解决方案资源管理器**"窗口中，右键单击 **.dtsx** ，然后选择"**重命名**"。 如果看不到**解决方案资源管理器**窗口，请单击菜单栏上的 "**视图**"，然后单击 "**解决方案资源管理器**"。

     ![Package.dtsx -“重命名”菜单](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package.dtsx -“重命名”菜单")

7.  键入**cleanseandcurate.cleanse supplier data.guid** ，然后按**enter**。 请确保该**扩展**保持为 " **.dtsx**"。

## <a name="next-step"></a>下一步
 [任务 5：添加数据流任务](task-5-adding-data-flow-task.md)


