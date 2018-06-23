---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 02c1104c6736572b0d2bfcd3783b0ef1b400fb20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127081"
---
# <a name="mssqlserver8992"></a>MSSQLSERVER_8992
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8992|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC3_CHECK_CATALOG|  
|消息正文|请检查目录消息 ERROR，级别 LEVEL，状态 STATE: MESSAGE。|  
  
## <a name="explanation"></a>解释  
 DBCC CHECKCATALOG 或 DBCC CHECKDB 在指定对象的系统元数据表中发现了不一致。 这就是说，已记录的对象 ID 与错误消息中指定的对象之间存在不一致。  
  
 如果通过某种方式手动更新一个或多个系统表，而该方式在系统元数据中造成了不一致，就会发生此错误。 例如，用户可能从 **sysobjects** 表中手动删除了某个对象，但未从 **sysindexes** 和 **syscolumns** 等其他表中删除关联的行。  
  
 在对已从 SQL Server 2000 升级至 SQL Server 2005 或更高版本的数据库运行 DBCC CHECKDB 时，也可能发生此错误。 在 SQL Server 2000 中，DBCC CHECKDB 并不包括 DBCC CHECKCATALOG 功能，因此升级前不会捕捉到此错误，除非专门针对 SQL Server 2000 中的数据库执行 DBCC CHECKCATALOG。  
  
 除错误 8992 外，还可能显示以下任一错误：  
  
 消息 3851 - 在系统表 sys.%ls%ls 中发现无效的行(%ls)。  
  
 消息 3852 - sys.%ls%ls 中的行(%ls)在 sys.%ls%ls 中没有匹配的行(%ls)。  
  
 3853 - sys.%ls%ls 中的行(%ls)的属性(%ls)在 sys.%ls%ls 中没有匹配的行(%ls)。  
  
 3854 - sys.%ls%ls 中的行(%ls)的属性(%ls)与 sys.%ls%ls 中的行(%ls)匹配，但该行无效。  
  
 3855 - 属性(%ls)存在，但 sys.%ls%ls 中没有行(%ls)。  
  
 3856 - 属性(%ls)存在，但它与 sys.%ls%ls 中的行(%ls)不匹配。  
  
 3857 - 缺少 sys.%ls%ls 中的行(%ls)所需的属性(%ls)。  
  
 3858 - sys.%ls%ls 中的行(%ls)的属性(%ls)具有无效的值。  
  
## <a name="user-action"></a>用户操作  
  
### <a name="drop-and-re-create-the-specified-object"></a>删除并重新创建指定的对象  
 如果可能，请删除并重新创建指定的对象。 例如，如果该对象是一个存储过程或用户定义类型，则重新创建该对象将可能解决该问题。  
  
### <a name="restore-from-backup"></a>从备份还原  
 如果出现的问题与硬件无关，并且您确信有可用的干净备份，请从备份中还原数据库。 只有备份中没有元数据错误时，此操作才适用。  
  
### <a name="export-the-data-to-a-new-database"></a>将数据导出到新数据库  
 如果备份还包含元数据不一致性，则您需要创建一个新的数据库，并将现有数据库的内容导出到这个新的数据库。  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>DBCC CHECKDB 无法修复此错误  
 无法修复此错误。  如果无法从备份还原数据库，请与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客户服务与支持部门 (CSS) 联系。  
  
### <a name="do-not-manually-update-system-tables"></a>不手动更新系统表  
 不对系统表进行手动更新。 SQL Server 不支持对系统数据库进行任何手动更改。 如果您更新 SQL Server 数据库中的系统表，则会记录两个事件（事件 ID 17659 和事件 ID 3859）。 有关详细信息，请参阅知识库文章 2688307：“当更新 SQL Server 数据库中的系统表时，将记录事件 ID 17659 和事件 ID 3859”。  
  
## <a name="see-also"></a>请参阅  
 [当更新 SQL Server 数据库中的系统表时，将记录事件 ID 17659 和事件 ID 3859](http://support.microsoft.com/kb/2688307/EN-US)  
  
  