---
title: 编辑类型映射 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 513f071a-d5e6-4ed5-acca-269bf76323c5
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 218f2450732a0374d0adeec0e28637d2e3fc449d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="edit-type-mapping-sybasetosql"></a>编辑类型映射 (SybaseToSQL)
**编辑类型映射**对话框中，可以指定类型的源和目标的数据库对象对象之间的映射方式。  
  
你可以访问此对话框中，在多个位置：  
  
-   当你选择源数据库或数据库对象**类型映射**选项卡上显示的元数据资源管理器的右侧。 单击**添加**以添加新的类型映射，或单击**编辑**若要更改现有的类型映射。  
  
-   上**工具**菜单上，选择**项目设置**或**默认项目设置**。 在生成的对话框中，选择**类型映射**。 单击**添加**以添加新的类型映射，或单击**编辑**若要更改现有的类型映射。  
  
特定于表的类型映射重写数据库和项目类型映射。 特定于数据库的映射覆盖项目映射。  
  
## <a name="options"></a>选项  
**源类型**  
选择要映射到的源数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型。  
  
以下字段的可变长度数据类型时，将出现在**源类型**:  
  
**从**  
指定此映射的最短长度。 例如，对于**nchar**数据类型，你可以输入 10 来指定此映射的范围开始**nchar(10)**。  
  
**若要**  
指定此映射的最大长度。 例如，对于**nchar**数据类型，你可以输入 20，若要指定此映射的结束时间范围**nchar(20)**。  
  
**目标类型**  
选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]源数据类型映射到的数据类型。 SSMA 时创建的表或存储的过程在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，源数据类型将更改为此数据类型。  
  
以下字段的可变长度数据类型时，将出现在**目标类型**:  
  
**Replace with**  
指定此映射的目标长度。 例如，对于**nvarchar**数据类型，你可以输入 20 指定指定的源数据类型应映射到**nvarchar(20)**。  
  
