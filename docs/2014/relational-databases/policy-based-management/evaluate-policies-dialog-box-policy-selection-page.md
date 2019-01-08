---
title: “评估策略”对话框 -“策略选择”页 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6266dd29c3486b6ae4163b15cffbc455eee31c5a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52780949"
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>“评估策略”对话框，“策略选择”页
  此对话框用于评估基于策略的管理策略。 选择 **“评估结果”** 页后，可以将策略应用于目标集中不符合这些策略的项。  
  
## <a name="options"></a>选项  
 **数据源**  
 指定策略的来源。 若要更改来源，请单击“浏览”按钮 (**...**) 以打开“选择源”对话框。  
  
 **“文件”**  
 键入包含基于策略的管理策略的文件的路径，或者使用“浏览”按钮 (**...**) 选择文件。  
  
 **Server**  
 选择此选项可连接到包含所需策略的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例。  
  
 **策略：策略**  
 单击可打开指定策略的“策略”对话框。  
  
 **策略：类别**  
 策略的类别。 此框是只读的。  
  
 **策略：分面**  
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
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来管理服务器](administer-servers-by-using-policy-based-management.md)   
 [“评估策略”对话框，“评估结果”页](evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
