---
title: 模拟信息 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42319d60-ccd0-46b8-af0b-f0968c390d8a
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 90a9d2102df9bd1b6cdf2bf1e4c7b3386c0fa825
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016999"
---
# <a name="impersonation-information"></a>模拟信息
  使用 **“模拟信息”** 页可以指定 Analysis Services 将用于连接到数据源的凭据。  
  
## <a name="options"></a>“常规”  
 **使用特定 Windows 用户名和密码**  
 选择此选项将使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象使用指定 Windows 用户帐户的安全凭据。 指定凭据将用于执行处理、ROLAP 查询、外部绑定、本地多维数据集、挖掘模型、远程分区、链接对象以及从目标到源的同步。 但是，对于数据挖掘扩展插件 (DMX) OPENQUERY 语句，则忽略此选项，并且将使用当前用户的凭据而不是指定用户帐户的凭据。  
  
 **用户名**  
 键入所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象将使用的用户帐户的域和名称。 使用以下格式：  
  
 *\<域名 >* **\\** *\<用户帐户名 >*  
  
 只有选定了 **“使用特定名称和密码”** ，才启用此选项。  
  
 **密码**  
 键入所选 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象将使用的用户帐户的密码。  
  
 只有选定了 **“使用特定名称和密码”** ，才启用此选项。  
  
 **使用服务帐户**  
 选择此选项将使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象使用与管理该对象的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务相关联的安全凭据。 服务帐户凭据将用于处理、ROLAP 查询、远程分区、链接对象以及从目标到源的同步。 但是，对于数据挖掘扩展插件 (DMX) OPENQUERY 语句、本地多维数据集和挖掘模型，将使用当前用户的凭据。 外部绑定不支持此选项。  
  
 **使用当前用户的凭据**  
 选择此选项将使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象使用当前用户的安全凭据来处理外部绑定、DMX OPENQUERY、本地多维数据集和挖掘模型。 处理、ROLAP 查询、远程分区、链接对象以及从目标到源的同步不支持此选项。  
  
 **继承**  
 选择此选项可以使用服务器管理员通过 `DataSourceImpersonation` 数据库属性设置的、在数据库级别定义的模拟行为。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的数据源](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支持的数据源&#40;SSAS 多维&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  