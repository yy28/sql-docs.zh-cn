---
title: “评估策略”对话框的“策略选择”页面
description: 介绍 SQL Server Management Studio (SSMS) 中基于策略的管理的“评估策略”对话框的“策略选择”页面。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f82a5b8760710f0d72554e1f0b5b083ccd58294c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749426"
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>“评估策略”对话框，“策略选择”页
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此对话框用于评估基于策略的管理策略。 选择 **“评估结果”** 页后，可以将策略应用于目标集中不符合这些策略的项。  
  
## <a name="options"></a>选项  
 **数据源**  
 指定策略的来源。 若要更改来源，请单击“浏览”按钮 ( **...** ) 以打开“选择源”  对话框。  
  
 **文件**  
 键入包含基于策略的管理策略的文件的路径，或者使用“浏览”按钮 ( **...** ) 选择文件。  
  
 **Server**  
 选择此选项可连接到包含所需策略的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例。  
  
 **策略: 策略**  
 单击可打开指定策略的“策略”对话框。  
  
 **策略: 类别**  
 策略的类别。 此框是只读的。  
  
 **策略: 方面**  
 策略所实现的方面。 此框是只读的。  
  
 **评估**  
 在评估模式下运行策略。 这会为目标集生成符合报告，但不会重新配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或强制要求以后符合策略。  
  
## <a name="possible-errors"></a>可能出现的错误  
  
-   **找不到目标**  
  
     由于任何以下原因，目标集可能为空：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上没有策略所指定类型的目标。  
  
    -   服务器限制可能排除包含目标的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
    -   如果策略位于数据库中的对象（如表、视图或用户）上，数据库可能不会订阅策略类别。  
  
    -   目标集筛选器可能排除此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上的所有目标。  
  
    -   目标服务器类型不同于在其中评估策略的服务器的类型。 例如，在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]中，如果尝试评估一个为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]创建的策略，则会收到一个空的目标集。  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [“评估策略”对话框，“评估结果”页](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
