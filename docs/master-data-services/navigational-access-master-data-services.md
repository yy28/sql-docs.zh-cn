---
description: 导航访问权限 (Master Data Services)
title: 导航访问权限
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- navigational access [Master Data Services]
- security [Master Data Services], navigational access
ms.assetid: 3403b7b0-44e2-48c3-a1b7-9c4612b874b8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bd1879ee534a3f17de39b1b632a0fcaeb835abbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88343113"
---
# <a name="navigational-access-master-data-services"></a>导航访问权限 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  导航访问权限适用于在 **“模型”** 选项卡上分配的模型对象安全性。  
  
 导航访问权限是所获得的高于已分配安全性级别的访问权限。  
  
 在本示例中，权限将分配给某一实体，因此在模型级别授予导航访问权限。  
  
 ![mds_conc_inheritance_model](../master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **实体**  
  
 在您向某一实体、其叶成员或其合并成员分配权限时，导航访问权限意味着您可以读取或更新所有成员的名称和代码。 您还可以读取模型名称。  
  
 **特性**  
  
 在您向某一属性分配权限时，导航访问权限意味着您可以读取或更新实体中所有成员的名称和代码。 您还可以读取模型名称。  
  
 **集合**  
  
 在您向集合分配权限时，您可以读取或更新名称、代码、说明和所有者 ID。 您还可以读取模型名称。  
  
## <a name="see-also"></a>另请参阅  
 [如何确定权限 (Master Data Services)](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
