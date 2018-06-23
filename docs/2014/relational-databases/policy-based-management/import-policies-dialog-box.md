---
title: “导入策略”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1d8bcdd179434c273c37ce2bb6a00d53ea7c75b0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026104"
---
# <a name="import-policies-dialog-box"></a>“导入策略”对话框
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
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来管理服务器](administer-servers-by-using-policy-based-management.md)   
 [导入基于策略的管理策略](import-a-policy-based-management-policy.md)   
 [导出基于策略的管理策略](export-a-policy-based-management-policy.md)  
  
  