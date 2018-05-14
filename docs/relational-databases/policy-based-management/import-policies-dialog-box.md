---
title: “导入策略”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0e672c7cfb95870236e6e6ed4601790fda6d0a87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="import-policies-dialog-box"></a>“导入策略”对话框
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此对话框可以将保存为 XML 文件的一个或多个策略（及其引用的条件）导入当前 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例。  
  
## <a name="options"></a>“常规”  
 **要导入的文件**  
 若要从 XML 文件导入策略，请键入该文件的路径和名称或者使用“浏览”(**...**) 按钮。  
  
 **用导入的项替换重复项**  
 如果选择此选项，当相同名称的任何现有策略或条件在此 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例上已存在时，则会覆盖这些内容。 无法覆盖具有依赖策略的条件，除非也覆盖该依赖策略。 如果未选择此选项，使用相同条件表达式的现有条件不会导致错误。  
  
 **策略状态**  
 为导入的策略选择所需的状态：  
  
-   **保留导入时的策略状态**  
  
-   **启用关于导入的所有策略**  
  
-   **禁用关于导入的所有策略**  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [导入基于策略的管理策略](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)   
 [导出基于策略的管理策略](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)  
  
  
