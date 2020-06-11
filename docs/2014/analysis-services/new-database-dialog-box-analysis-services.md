---
title: "\"新建数据库\" 对话框（Analysis Services） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.newdatabase.f1
ms.assetid: ddc7804b-acb0-4ae4-a88f-e8cdf704c341
author: minewiskan
ms.author: owend
ms.openlocfilehash: 07eeee6136965671b000923dc3f240de06ce0bd0
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541179"
---
# <a name="new-database-dialog-box-analysis-services"></a>“新建数据库”对话框 (Analysis Services)
  可以使用 **中的** “新建数据库” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 对话框创建新的空 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。 通过在对象资源管理器中右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的“数据库”文件夹，并选择“新建数据库”，可以显示“新建数据库”对话框。****************  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**数据库名称**|键入新 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的名称。|  
|**使用特定用户名和密码**|选择此选项可以使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库使用指定用户帐户的安全凭据。 指定凭据将用于执行处理、ROLAP 查询、外部绑定、本地多维数据集、挖掘模型、远程分区、链接对象以及从目标到源的同步。 但是，对于 DMX OPENQUERY 语句，将使用当前用户的凭据。|  
|**用户名**|键入所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库将使用的用户帐户的域和名称。 使用以下格式：<br /><br /> *\<Domain name>* **\\** *\<User account name>*<br /><br /> 注意：仅当已选择“使用特定用户名和密码”时，才会启用此选项。 ****|  
|**密码**|键入在 **“用户名”** 中指定的用户帐户的密码。|  
|**使用服务帐户**|选择此选项可以使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库使用与管理数据库的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务关联的安全凭据。 服务帐户凭据将用于处理、ROLAP 查询、远程分区、链接对象以及从目标到源的同步。 对于 DMX OPENQUERY 语句、本地多维数据集和挖掘模型，将使用当前用户的凭据。 外部绑定不支持此选项。|  
|**使用当前用户的凭据**|选择此选项将使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库使用当前用户的安全凭据来处理外部绑定、DMX OPENQUERY 语句、本地多维数据集和挖掘模型。 处理、ROLAP 查询、远程分区、链接对象以及从目标到源的同步不支持此选项。|  
|**默认**|选择此选项可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的默认用户帐户的凭据。 此选项使用数据库的默认设置来处理对象、同步服务器以及执行 **Open Query** 数据挖掘语句。 有关在数据库级别指定默认设置的详细信息，请参阅[设置多维数据库属性 (Analysis Services)](multidimensional-models/set-multidimensional-database-properties-analysis-services.md)。<br /><br /> 默认情况下，" `DataSourceImpersonationInfo` 数据库属性" 设置为 **"使用服务帐户"**。 无论 `DataSourceImpersonationInfo` 属性值如何，均会将当前用户的凭据用于外部绑定、ROLAP 查询、本地多维数据集和数据挖掘模型。|  
|**说明**|键入新 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的说明。|  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多维模型数据库 (SSAS)](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
