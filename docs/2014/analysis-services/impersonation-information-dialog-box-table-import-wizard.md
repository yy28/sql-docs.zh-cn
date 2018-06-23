---
title: 模拟信息对话框 （表导入向导） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.impersonationinfo.f1
ms.assetid: bee7eee5-0650-41f1-a372-5076ae97a58c
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c53b71a06904bd3f898efa3dd2d9946670193845
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124220"
---
# <a name="impersonation-information-dialog-box-table-import-wizard"></a>“模拟信息”对话框（表导入向导）
  使用 **“模拟信息”** 页可以指定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将用于连接到数据源的凭据。 有关凭据模拟的详细信息，请参阅[模拟&#40;SSAS 表格&#41;](tabular-models/impersonation-ssas-tabular.md)。  
  
## <a name="options"></a>“常规”  
 **特定 Windows 用户名和密码**  
 选择此选项将使表格模型使用指定的 Windows 用户帐户的安全凭据。  
  
 **用户名**  
 键入要使用的用户帐户的域和名称。 使用以下格式：  
  
 *\<域名 >* **\\** *\<用户帐户名 >*  
  
 只有选定了 **“使用特定名称和密码”** ，才启用此选项。  
  
 **密码**  
 键入表格模型将使用的用户帐户的密码。  
  
 只有选定了 **“使用特定名称和密码”** ，才启用此选项。  
  
 **服务帐户**  
 选择此选项将使用与管理该模型的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务相关联的安全凭据。  
  
## <a name="see-also"></a>请参阅  
 [模拟&#40;SSAS 表格&#41;](tabular-models/impersonation-ssas-tabular.md)  
  
  