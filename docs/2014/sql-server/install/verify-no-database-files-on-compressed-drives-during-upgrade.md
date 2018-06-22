---
title: 验证在升级过程中没有任何数据库文件是否在压缩驱动器上 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 59370b953c377e983f58c3037a7920de0076bd56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014459"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>确保升级过程中压缩驱动器上没有任何数据库文件
  升级顾问检测到压缩驱动器上有数据库文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法在压缩驱动器上创建或升级数据库。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，请为系统数据库选择非压缩驱动器，并验证要升级的数据库不在压缩驱动器上。 但是，请注意，在数据库升级之后，可以将只读数据库和只读辅助文件组放在 NTFS 压缩文件系统中。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
