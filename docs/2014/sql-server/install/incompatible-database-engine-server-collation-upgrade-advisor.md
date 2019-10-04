---
title: 不兼容数据库引擎服务器排序规则（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fbd4c1e55bb49c6ae8f75d3d12cc243df963018a
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952233"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>不兼容的数据库引擎服务器排序规则（升级顾问）
  升级顾问检测到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] @no__t 使用配置为使用不兼容服务器排序规则的 @no__t 的实例。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 升级顾问检测到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] @no__t 使用配置为使用不兼容服务器排序规则的 @no__t 的实例。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式利用 SharePoint 共享服务体系结构。 SharePoint 不支持为区分大小写的服务器排序规则或二进制排序规则配置的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 不兼容的排序规则包括默认区分大小写或为二进制的排序规则，以及默认兼容但使用任何以下排序规则指示符配置的基本排序规则：  
  
-   **Binary**  
  
-   **区分大小写**  
  
-   **Binary-codepoint**  
  
 因为当前 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服务器排序规则不兼容，所以升级被阻止。  
  
## <a name="corrective-action"></a>纠正措施  
 不能更改 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服务器排序规则属性。 您将不能完成 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的升级。 您将需要将您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装迁移到正在使用兼容的服务器排序规则的新服务器。 有关详细信息，请参见以下内容：  
  
-   [升级和迁移 Reporting Services](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [选择 SQL Server 排序规则](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
