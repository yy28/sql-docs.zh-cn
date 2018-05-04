---
title: 编辑类型映射 (DB2ToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f93c4b7d-74fc-4856-bf42-035289918e83
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fc0c8b753d6be25702bbba61fccae154701a7816
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="edit-type-mapping-db2tosql"></a>编辑类型映射 (DB2ToSQL)
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
  
