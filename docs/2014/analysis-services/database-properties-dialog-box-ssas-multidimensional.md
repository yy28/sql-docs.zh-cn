---
title: 数据库属性对话框 (SSAS-多维) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.databaseproperties.f1
ms.assetid: 70f000b7-917f-4699-b142-7a0d13ff767c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be4133aa143ecf0e1fb9b50c40a38a73b4207f30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082320"
---
# <a name="database-properties-dialog-box-ssas---multidimensional"></a>“数据库属性”对话框（SSAS - 多维）
  可以使用 **中的** “数据库属性” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 对话框设置 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的属性。 在对象资源管理器中右键单击某个数据库，并选择“属性”，可以显示“数据库属性”对话框   。  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**名称**|键入内容即可更改数据库的名称。|  
|**ID**|显示数据库的标识符。|  
|**说明**|键入内容即可更改数据库的说明。|  
|**创建时间戳**|显示数据库的创建日期和时间。|  
|**上次架构更新时间**|显示上次更新数据库元数据的日期和时间。|  
|**上次更新时间**|显示上次更新数据库的日期和时间。|  
|**数据源模拟信息**|选择在连接到数据库中包含的数据源以及与该数据源进行交互时数据库所使用的模拟信息。 包括以下有效值：<br /><br /> **ImpersonateAccount** （使用特定的 Windows 用户名和密码）。<br /><br /> **ImpersonateService** （使用服务帐户）。<br /><br /> **ImpersonateCurrentUser** （使用当前用户的凭据）。<br /><br /> **默认值** （使用服务帐户执行 MOLAP 操作，使用当前用户执行数据挖掘）。<br /><br /> 尽管您可以在数据库级别设置数据源模拟设置，但这样做只影响为其模拟设置指定 **“继承”** 的那些数据源。 直接在数据源上指定的模拟设置始终覆盖在数据库级别指定的任何设置。<br /><br /> 当选择模拟选项时，请考虑需要支持的操作类型。 无法执行某些操作（如处理）|  
|**上次处理**|显示上次处理数据库的日期和时间。|  
|**估计的大小**|显示数据库的估计大小。|  
|**存储位置**|指定数据库的位置。 如果数据库位于默认数据目录中，则此值将为空。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多维模型数据库 (SSAS)](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
