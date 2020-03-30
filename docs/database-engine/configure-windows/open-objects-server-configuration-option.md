---
title: open objects 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- open objects option
ms.assetid: c8424d3c-86ba-4cc5-bf0c-be4ce44bdd04
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 526a196c280e4a8b62db27be4c8644315379b2d3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67997943"
---
# <a name="open-objects-server-configuration-option"></a>open objects 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  尽管在   中已禁用此选项的功能，但此选项仍然存在于 sp_configure 中[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 （其设置不起作用。）在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，打开的数据库对象的数量是动态管理的，该数量只受可用内存的限制。 **sp_configure** 中可用的 **open objects** 选项用于现有脚本的后向兼容性。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
