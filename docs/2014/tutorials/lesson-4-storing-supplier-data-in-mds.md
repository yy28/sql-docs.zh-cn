---
title: 第4课：在 MDS 中存储供应商数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: bacd9eaf-4d12-4f25-aec7-d785dec1b623
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 678a7d6ce075e6a1082856aa7962bb3f6eec522d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489711"
---
# <a name="lesson-4-storing-supplier-data-in-mds"></a>第 4 课：在 MDS 中存储供应商数据
  Master Data Services (MDS) 是用于主数据管理的 SQL Server 解决方案。 主数据管理 (MDM) 描述组织为发现和定义数据的非事务性列表而付出的努力。  
  
 模型是 Master Data Services 中最高的组织级别，负责整理主数据的结构。 您的 MDS 实现可以具有一个或多个模型，其中每个模型对相似的数据进行分组。 通常，可通过以下四种方式之一划分主数据：人员、地点、事件或概念。 例如，可以创建 Product 模型来包含与产品有关的数据，或创建 Customer 模型来包含与客户有关的数据。 有关更多详细信息，请参阅[模型（Master Data Services）](https://msdn.microsoft.com/library/ee633746.aspx) 。  
  
 模型可以包含一个或多个实体。 每个实体具有属性（列）和成员（行）。 每行都包含主数据。 在本课中，您将创建一个 Suppliers 模型，其中具有两个实体，名称分别为 Supplier 和 State。 Supplier 实体将具有以下属性：Code、Name、Contact First Name、Contact Last Name、Contact Email Address、Address Line、City、State、Zip 和 Country。 有关属性的详细信息，请参阅[属性（Master Data Services）](https://msdn.microsoft.com/library/ee633745.aspx) 。 Code 和 Name 属性分别对应于 Excel 文件 (Cleansed and Matched Suppliers) 中的 SupplierID 和 Supplier Name 列。  
  
 基于域的属性是指其值由另一个实体的成员填充的属性。 基于域的属性可防止用户输入无效的属性值。 只能从由另一个实体填充的下拉列表中选择属性值。 在本教程中，Supplier 实体的 State 属性是一个基于域的属性，其值来自 State 实体。 您只可将 Supplier 实体的 State 属性的值更改为 State 实体中的一个值。 有关更多详细信息，请参阅[基于域的属性](../master-data-services/domain-based-attributes-master-data-services.md)。  
  
 MDS 中的派生层次结构派生自模型中基于域的属性关系。 在本教程中，您将在 Supplier 实体和 State 实体之间创建一个派生层次结构。 在创建派生层次结构后，您将在主数据管理器的浏览器中看到州的列表。 当您单击列表中的某个州时，您将在右窗格中看到该州的供应商。 随后，您将基于此关系创建派生层次结构。 有关更多详细信息，请参阅[派生层次结构](../master-data-services/derived-hierarchies-master-data-services.md)。  
  
 您在 DQS 中构建了一个知识库，并使用此知识库来清理和匹配供应商数据，然后将结果存储在 Cleansed and Matched Supplier Data.xls 文件中。 在本课中，您要将清理和匹配的数据上载到 MDS 中。 DQS 只包含有关数据（元数据）的知识，而 MDS 存储数据本身（主数据集）。 例如：DQS 可能具有有关多个供应商的知识，但 MDS 只维护公司所使用的供应商。  
  
 在本课中，您将执行以下任务：  
  
1.  使用**主数据管理器 Web 应用程序**在**MDS**中创建**供应商**模型。  
  
2.  在 Excel 中打开**清理和匹配的供应商数据**，并使用**MDS Add-in for Excel**创建一个名为 "**供应商**" 的实体，然后将数据上载到 MDS。  
  
3.  使用**主数据管理器**验证是否在 MDS 中创建了数据。  
  
4.  创建一个名为**State**的实体，并将**供应商**实体的**state**属性更新为基于域的属性，具体取决于**State**实体。 使用**MDS Add-in for Excel**执行此操作。  
  
5.  验证是否使用**主数据管理器**创建了基于域的属性，并更新 "**状态**" 实体的 "**名称**" 属性的值。  
  
6.  使用在**Excel****主数据管理器**中查看所做的更新。  
  
7.  将值从**状态**实体加载到**Excel**中并添加值，并使用**主数据管理器**验证加法。  
  
8.  通过使用 "**供应商**" 实体与 "**状态**" 实体（供应商实体的 "状态" 属性为 "状态" 实体类型**主数据管理器**）之间的基于域的属性关系创建和使用派生层次结构。  
  
## <a name="next-step"></a>下一步  
 [任务 1：使用主数据管理器创建供应商模型](../../2014/tutorials/task-1-creating-suppliers-model-using-master-data-manager.md)  
  
  
