---
title: 数据库属性对话框 (SSAS-表格) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.DatabaseProperties.f1
ms.assetid: 0f0ec02f-7b55-40ea-8a04-ed0deb1efd7a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8361508d678e407be9bed6eb18e8c221364daf61
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082355"
---
# <a name="database-properties-dialog-box-ssas---tabular"></a>“数据库属性”对话框（SSAS - 表格）
  此对话框提供了时间戳和其他说明性信息，以及确定数据库是否使用缓存数据的可自定义属性。 其他可自定义的属性包括更改数据库名称和指定模拟选项。  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**名称**|**“名称”** 是唯一标识服务器上的数据库的数据库名称。 在更改数据库名称时，应考虑对在现有连接字符串中使用当前名称的报表和客户端应用程序的影响。 您将需要在现有报表中更新连接字符串，以便避免拒绝访问错误。 此外，作为此数据库的源的表格模型最有可能使用原始名称。 请考虑更新模型中的数据库部署属性，以便确保对该模型的将来的更新发布到所需数据库。|  
|**ID**|显示数据库的标识符。|  
|**说明**|键入内容即可更改数据库的说明。|  
|**创建时间戳**|显示数据库的创建日期和时间。|  
|**上次架构更新时间**|显示上次更新数据库元数据的日期和时间。|  
|**上次更新时间**|显示上次更新数据库的日期和时间。|  
|**读写模式**|这是一个只读属性，但你可以使用 **Detach** 和 **Attach** 命令序列更改该属性，其中该属性是 **Attach** 命令的参数。 有关详细信息，请参阅 [数据库 ReadWriteMode](multidimensional-models/database-readwritemodes.md)。|  
|**DirectQueryMode**|指定数据库是只使用内存中存储（没有磁盘存储）、只使用基于磁盘的存储还是结合使用这两种存储。 有效值是 InMemory、DirectQuery、InMemoryWithDirectQuery（主要基于内存，但具有某些磁盘分页）或 DirectQueryWithInMemory（主要基于磁盘，但具有一些内存中存储）。 有关详细信息，请参阅[DirectQuery 部署方案&#40;SSAS 表格&#41;](directquery-deployment-scenarios-ssas-tabular.md)。|  
|**数据源模拟信息**|指定在处理或刷新本地或远程分区上的数据时用于数据库连接的模拟帐户、针对关系数据存储区（通过 DirectQuery）运行的查询、外部绑定以及从目标到源的数据库同步。<br /><br /> 有效值包括 Analysis Services 服务帐户或一组特定的 Windows 凭据。 不要指定 **“使用当前用户的凭据”**。 表格模型数据库不支持该凭据选项。|  
|**上次处理**|显示上次处理数据库的日期和时间。|  
|**估计的大小**|显示数据库的估计大小。|  
|**存储位置**|指定数据库的位置。 如果数据库位于默认数据目录中，则此值将为空。|  
  
  
