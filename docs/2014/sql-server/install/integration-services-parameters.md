---
title: Integration Services 参数 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f178c02cc93d23a14e0fb658398e5f0ba4cf6dc0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024714"
---
# <a name="integration-services-parameters"></a>Integration Services 参数
  有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，你可以决定分析[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包的计算机上，或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]文件打包的文件系统中。 如果分析文件系统中的文件，则需要提供包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的文件夹的路径。  
  
## <a name="options"></a>“常规”  
 **分析计算机上的 SSIS 包**  
 选择此选项可分析计算机上 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 默认情况下，将选中此选项。  
  
 **分析 SSIS 包文件**  
 选择此选项可分析文件系统中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
 **SSIS 包的路径**  
 找到包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的 UNC 或本地路径。 不必包含文件名。 如果无法访问你输入的路径，则不能单击**下一步**。 默认情况下，此路径为空。 仅当你选择启用此字段**分析 SSIS 包文件**。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  