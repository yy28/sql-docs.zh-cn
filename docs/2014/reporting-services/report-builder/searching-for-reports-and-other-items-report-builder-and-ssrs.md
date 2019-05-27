---
title: 搜索报表和其他项（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6a586659-5c2b-453b-8f40-a3a469277b17
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 76746ade9222257bcea6962c180ea12a01ff8afa
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107653"
---
# <a name="searching-for-reports-and-other-items-report-builder--and-ssrs"></a>搜索报表和其他项（报表生成器和 SSRS）
  您可以使用报表管理器在报表服务器中按名称或说明搜索特定的项。 可以搜索发布的报表、报表模型、文件夹、共享数据源和资源。 无法搜索计划、所有者、角色分配、订阅或者报表历史记录中的特定快照。 搜索是在存储项的报表服务器数据库上执行的。  
  
> [!NOTE]  
>  对于由报表服务器管理的项，执行文件系统搜索不会为其返回搜索结果。  
  
-   若要在报表管理器中搜索项，请在页面顶部的 **“搜索”** 文本框中键入搜索字符串。 搜索将从文件夹层次结构的顶部节点开始，然后逐渐涉及每一个分支。 如果您无权访问特定分支，就会将其跳过。 这一点适用于其他用户的“我的报表”文件夹以及一般情况下不可用的其他文件夹。 搜索结果中将只包含您有权查看的报表和项。  
  
-   若要按名称或说明搜索项，请指定希望匹配的全部或部分文本。 搜索字符串不区分大小写。 不能使用搜索运算符来规定或排除搜索条件，如加号 (+) 或减号 (-)。  
  
-   若要在报表中搜索特定文本，请使用报表顶部的工具栏。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [在报表管理器中查找和查看报表（报表生成器和 SSRS）](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)   
 [使用“我的报表”（报表生成器和 SSRS）](using-my-reports-report-builder-and-ssrs.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [打开和关闭报表（报表管理器）](../reports/open-and-close-a-report-report-manager.md)  
  
  
