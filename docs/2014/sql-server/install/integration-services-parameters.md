---
title: Integration Services 参数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 100e796bb27d1e60db000a364a0432273dd5cafb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094236"
---
# <a name="integration-services-parameters"></a>Integration Services 参数
  对于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，你可以决定分析[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]计算机上的包或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]文件系统中的包文件。 如果分析文件系统中的文件，则需要提供包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的文件夹的路径。  
  
## <a name="options"></a>选项  
 **分析计算机上的 SSIS 包**  
 选择此选项可分析计算机上 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 默认情况下，将选中此选项。  
  
 **分析 SSIS 包文件**  
 选择此选项可分析文件系统中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
 **SSIS 包的路径**  
 找到包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的 UNC 或本地路径。 不必包含文件名。 如果你输入的路径无法访问，则无法单击 "**下一步**"。 默认情况下，此路径为空。 仅当选择 "**分析 SSIS 包文件**" 时，才会启用此字段。  
  
## <a name="see-also"></a>另请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
