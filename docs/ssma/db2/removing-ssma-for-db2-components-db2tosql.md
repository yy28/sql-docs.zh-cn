---
title: 删除 SSMA for DB2 组件 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d4f819a92885cf5d173bcdda53ebf3291c958eac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270113"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>删除 SSMA for DB2 组件 (DB2ToSQL)
完成后将数据库迁移在 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可能需要卸载 SSMA 组件。 您可以在任何时候卸载客户端组件。 但是，不应卸载扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非你已迁移的数据库不能再使用中的函数**ssma_DB2**的架构**sysdb**数据库。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>卸载 SSMA for DB2 客户端  
您可以通过使用卸载 SSMA**添加或删除程序**。  
  
**若要卸载的 SSMA**  
  
1.  在控制面板中，打开**添加或删除程序**。  
  
2.  选择 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**，然后单击**删除**。  
  
3.  若要确认你想要卸载 SSMA，请单击**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸载扩展包  
如果您确信你迁移的数据库不使用中的对象**sysdb.ssma_DB2**架构，您可以通过删除架构中删除的扩展包-有是没有 Windows 卸载  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for DB2 客户端&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SQL Server 上安装 SSMA 组件&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
