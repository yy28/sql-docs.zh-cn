---
title: 删除 DB2 组件的 SSMA （DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 25c8222009c2ea9358c0bab2ad5ae077588fb3cb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060101"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>删除 DB2 组件的 SSMA （DB2ToSQL）
完成将数据库从 DB2 迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之后，你可能想要卸载 SSMA 组件。 你可以随时卸载客户端组件。 但是，除非您迁移的数据库不再使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysdb**数据库的**ssma_DB2**架构中的函数，否则不应从卸载扩展包。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>卸载 DB2 客户端的 SSMA  
可以使用 "**添加或删除程序**" 卸载 SSMA。  
  
**卸载 SSMA**  
  
1.  在“控制面板”中，打开“添加或删除程序”  。  
  
2.  ** [!INCLUDE[msCoName](../../includes/msconame_md.md)]选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "迁移助手**"，然后单击 "**删除**"。  
  
3.  若要确认是否要卸载 SSMA，请单击 **"是"**。  
  
## <a name="uninstalling-the-extension-pack"></a>正在卸载扩展包  
如果你确定已迁移的数据库不使用**ssma_DB2 sysdb**架构中的对象，则可以通过将其从架构中删除来删除扩展包-无 Windows 卸载  
  
## <a name="see-also"></a>另请参阅  
[安装 SSMA for DB2 Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[在 SQL Server 上安装 SSMA 组件 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
