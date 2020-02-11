---
title: 管理对数据源视图和数据源所做的更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data sources
- modifying data source views
- data source views [Analysis Services], schema updates
- data sources [Analysis Services], schema updates
ms.assetid: 928c9f63-365a-43fd-9bbd-78828cc7e54d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac551a708433e973ada499f0e7504bc75516e756
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074771"
---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>管理对数据源视图和数据源所做的更改
  在重新运行架构生成向导时，它重用初始生成使用的相同数据源和数据源视图。 如果您添加数据源或数据源视图，则向导不会使用该数据源或数据源视图。 如果您在初始生成后删除原始数据源或数据源视图，则必须从头运行向导。 向导中的所有先前设置也会被删除。 下次运行架构生成向导时，基础数据库中任何绑定到已删除数据源或数据源视图的现有对象都被视为用户创建的对象。  
  
 如果数据源视图并未反映基础数据库生成时的实际状态，则架构生成向导在生成主题区域数据库架构时可能会遇到错误。 例如，如果数据源视图指定列的数据类型为 **int**，但该列的数据类型实际为 **string**，则架构生成向导会将外键的数据类型设置为 **INT** 以便与数据源视图相匹配，而在创建关系时会失败，因为实际类型为 **string**。  
  
 另一方面，如果您将数据源连接字符串更改为先前生成的其他数据库，则不会生成任何错误。 将会使用新的数据库，并且不会对先前数据库进行任何更改。  
  
## <a name="see-also"></a>另请参阅  
 [了解增量生成](understanding-incremental-generation.md)  
  
  
