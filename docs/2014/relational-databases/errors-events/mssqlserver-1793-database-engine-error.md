---
title: MSSQLSERVER_1793 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3d16cb776f9c908beaf59c70b2b519f9033e9fb0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412626"
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1793|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|FILESTREAM_BASEDATA_NEED_SAME_PARTITION|  
|消息正文|由于没有为 FILESTREAM 数据指定分区方案，因此无法删除索引“%.*ls”。|  
  
## <a name="explanation"></a>解释  
 当你尝试在包含 FILESTREAM 数据的表上删除聚集索引，并且为基础数据指定了 **MOVE TO** 子句，但没有为 FILESTREAM 数据指定 **FILESTREAM_ON** 子句时，将出现此消息。  
  
## <a name="user-action"></a>用户操作  
 在删除包含 FILESTREAM 数据的表上的聚集索引时，使用下列选项之一：  
  
-   为基础数据指定 **MOVE TO** 子句并且为 FILESTREAM 数据指定 **FILESTREAM_ON** 子句。  
  
-   不为基础数据指定 **MOVE TO** 子句，也不为 FILESTREAM 数据指定 **FILESTREAM_ON** 子句。  
  
 下面的示例失败，因为为基础数据指定了分区方案，但没有为 FILESTREAM 数据指定。  
  
```tsql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
 下面的示例成功，因为既为基础数据指定了 **MOVE TO** 子句，又为 FILESTREAM 数据指定了 **FILESTREAM_ON** 子句。  
  
```tsql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
 下面的示例也成功，因为既没有为基础数据指定 **MOVE TO** 子句，也没有为 FILESTREAM 数据指定 **FILESTREAM_ON** 子句。  
  
```tsql  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  
  
