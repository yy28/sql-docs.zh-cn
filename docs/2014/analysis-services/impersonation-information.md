---
title: 模拟信息 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 42319d60-ccd0-46b8-af0b-f0968c390d8a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05236d05e1b543ea7acb36f0856083e1c1db77a3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730672"
---
# <a name="impersonation-information"></a>模拟信息
  使用 **“模拟信息”** 页可以指定 Analysis Services 将用于连接到数据源的凭据。  
  
## <a name="options"></a>选项  
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
  
 **Inherit**  
 选择此选项可以使用服务器管理员通过 `DataSourceImpersonation` 数据库属性设置的、在数据库级别定义的模拟行为。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的数据源](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支持的数据源&#40;SSAS 多维&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
