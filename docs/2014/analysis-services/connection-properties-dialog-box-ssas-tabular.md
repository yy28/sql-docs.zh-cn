---
title: 连接属性对话框 (SSAS-表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3322b71162b93204591dbb1c0bffb6bac4856454
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148392"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>“连接属性”对话框（SSAS - 表格）
  使用此页可在 SQL Server Management Studio 中查看或修改表格模型数据库使用的数据源的连接属性。  
  
 此对话框提供了时间戳和其他说明性信息，以及确定连接特性的可自定义属性。  
  
## <a name="options"></a>“常规”  
  
|术语|定义|  
|----------|----------------|  
|**名称**|指定数据源的名称。|  
|**ID**|显示数据源对象的标识符。|  
|**Description**|显示数据源对象的说明。|  
|**创建时间戳**|显示数据库的创建日期和时间。|  
|**上次架构更新时间**|显示上次更新数据库元数据的日期和时间。|  
|**连接字符串**|显示用于连接到向模型提供数据的数据源的连接字符串。|  
|**最大连接数**|指定与此数据库之间的最大客户端连接数。|  
|**隔离**|有效值为 ReadCommitted 或 Snapshot。 有关详细信息，请参阅 [Isolation 元素 (ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/isolation-element-assl)。|  
|**查询超时值**|指定一段时间（以秒为单位），在这段时间过后试图检索数据时发生超时。|  
|**托管提供程序**|指定托管访问接口的名称。 如果数据源连接使用本机 OLE DB 访问接口，则此值为空。|  
|**模拟信息**|指定在处理或刷新数据时用于数据库连接的模拟帐户、针对关系数据存储区（通过 DirectQuery）运行的查询、外部绑定、远程分区以及从目标到源的数据库同步。<br /><br /> 有效值包括 Analysis Services 服务帐户或一组特定的 Windows 凭据。 不要指定 **“使用当前用户的凭据”** 或 **“继承”**。 表格模型数据库不支持这些凭据选项。|  
  
  
