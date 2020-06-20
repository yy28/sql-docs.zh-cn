---
title: 默认情况下，用于 SQL Server 的 Microsoft 全文引擎将不会加载未签名的第三方组件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 12ff188fb6aa6ac286817a7cc1c3ad726483c886
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012475"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a>Microsoft SQL Server 全文引擎在默认情况下不加载未签名的第三方组件
  默认情况下，[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文引擎将不加载未经 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 签名的组件。  
  
## <a name="component"></a>组件  
 全文搜索  
  
## <a name="description"></a>说明  
 默认情况下，在升级后 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文引擎将不加载服务器上当前已安装的第三方筛选器，如 PDF 筛选器。  
  
## <a name="corrective-action"></a>纠正措施  
 若要加载第三方筛选器，必须在该实例上设置*load_os_resource*并关闭*verify_signature* 。  
  
## <a name="see-also"></a>另请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
