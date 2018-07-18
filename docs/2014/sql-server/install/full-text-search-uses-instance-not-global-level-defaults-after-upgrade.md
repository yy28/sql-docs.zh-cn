---
title: 升级将导致全文搜索在默认情况下使用实例层级，而非全局，断字符和筛选器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 45ee5f8235aa79773bf3e92156701e47092c61c9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37311217"
---
# <a name="upgrading-will-cause-full-text-search-to-use-instance-level-not-global-word-breakers-and-filters-by-default"></a>升级将导致全文搜索在默认情况下使用实例级(而非全局)的断字符和筛选器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一种方法，允许在实例级别注册新的断字符和筛选器。  
  
## <a name="component"></a>组件  
 全文搜索  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许注册实例级的新的断字符和筛选器。 这种实例级注册提供了实例间的功能隔离和安全隔离。  
  
## <a name="corrective-action"></a>纠正措施  
 升级后，使用 `sp_fulltext_service` 设置服务属性和 `load_os_resources`，以便允许加载组件。 必须运行以下命令：  
  
 `sp_fulltext_service 'load_os_resources', 1`  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
