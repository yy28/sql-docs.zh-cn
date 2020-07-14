---
title: open objects 服务器配置选项 | Microsoft Docs
description: 了解“打开对象”这一已禁用的配置选项。 了解 SQL Server 现在如何管理打开的数据库对象的数量。
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0bbcb11a80f06eae10e5481c965e9216cc84695e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773624"
---
# <a name="open-objects-server-configuration-option"></a>open objects 服务器配置选项
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  尽管在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中已禁用此选项的功能，但此选项仍然存在于 sp_configure 中。 （其设置不起作用。）在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，打开的数据库对象的数量是动态管理的，该数量只受可用内存的限制。 **sp_configure** 中可用的 **open objects** 选项用于现有脚本的后向兼容性。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
