---
title: 准备命令 |Microsoft 文档
description: 准备使用的 SQL Server OLE DB 驱动程序的命令
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- prepared statements [OLE DB Driver for SQL Server]
- commands [OLE DB]
- command preparation [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55dd38bef585a473f7c84504d9d0263808e099b8
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="preparing-commands"></a>准备命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序支持命令准备用于优化多个执行单个命令;但是，命令准备生成开销，并使用者不需要准备要不止一次执行的命令。 一般而言，如果命令的执行次数超过三次，则应当进行准备。  
  
 出于性能方面的考虑，命令准备会延迟至命令执行之时。 这是默认行为。 待准备命令中的任何错误，直到执行命令或执行元属性操作时才会发现。 将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 属性 SSPROP_DEFERPREPARE 设置为 FALSE 可以关闭此默认行为。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，直接执行命令（即不提前准备命令）时，会创建并缓存一个执行计划。 如果再次执行该 SQL 语句，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 会采用有效的算法将新的语句与缓存中的现有执行计划进行匹配，然后再次使用该语句的执行计划。  
  
 对于准备好的命令，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 为准备和执行命令语句提供了本机支持。 在准备语句时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建一个执行计划，进行缓存，然后将该执行计划的句柄返回访问接口。 随后，访问接口使用该句柄来重复执行该语句。 不创建存储过程。 由于句柄会直接识别 SQL 语句的执行计划，而不用将语句与缓存中的现有语句进行匹配（如直接执行那样），因此，如果知道语句将多次执行，那么准备语句比直接执行语句更高效。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，无法使用预定义语句创建临时对象，也无法引用创建临时对象（如临时表）的系统存储过程。 必须直接执行这些过程。  
  
 始终不应准备某些命令。 例如，不应对指定存储过程执行的命令进行准备，也不应准备包含对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程创建无效的文本的命令。  
  
 如果创建临时存储的过程，则 SQL Server 的 OLE DB 驱动程序将执行的临时存储的过程，返回的结果，就像已执行语句本身。  
  
 临时存储的过程创建受 SQL Server OLE DB 驱动程序的特定初始化属性 SSPROP_INIT_USEPROCFORPREP。 如果属性值为 SSPROPVAL_USEPROCFORPREP_ON 或 SSPROPVAL_USEPROCFORPREP_ON_DROP，SQL Server 的 OLE DB 驱动程序将尝试在准备命令时创建的存储的过程。 如果应用程序用户拥有足够的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 权限，存储过程将创建成功。  
  
 对于不经常断开连接的用户来说，创建的临时存储过程可能需要大量资源的**tempdb**、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在其中创建临时对象的系统数据库。 时 SSPROP_INIT_USEPROCFORPREP 的值为 SSPROPVAL_USEPROCFORPREP_ ON 时，仅当创建命令的会话中失去其连接到的实例时，才会被丢弃为SQLServer创建的OLEDB驱动程序的临时存储的过程[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 如果该连接为数据源初始化时创建的默认连接，则临时存储过程仅当数据源变成未初始化状态时才删除。  
  
 SSPROPVAL_USEPROCFORPREP_ON_DROP SSPROP_INIT_USEPROCFORPREP 的值时，发生以下某种情况时，会删除的 OLE DB 驱动程序的 SQL Server 临时存储过程：  
  
-   使用者使用**ICommandText::SetCommandText**以指示新的命令。  
  
-   使用者使用**ICommandPrepare::Unprepare**以指示它不再需要的命令文本。  
  
-   使用者使用临时存储过程释放对命令对象的所有引用。  
  
 命令对象中具有最多一个临时存储的过程**tempdb**。 任何现有的临时存储过程都表示特定命令对象的当前命令文本。  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
