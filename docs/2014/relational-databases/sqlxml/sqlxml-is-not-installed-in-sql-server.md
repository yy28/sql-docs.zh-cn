---
title: SQL Server 中未安装 SQLXML |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fe1d4b937e5972eb90e567ded91f7a23af577d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012162"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQL Server 中未安装 SQLXML
  在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前，SQLXML 4.0 随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起发布，是所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本（[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 除外）默认安装的一部分。 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不再包括 SQLXML 的最新版本 (SQLXML 4.0 SP1)。 若要安装 SQLXML 4.0 SP1 可用时，将其从下载[SQLXML SP1 的安装位置](https://www.microsoft.com/download/details.aspx?id=16978)。  
  
 当某个应用程序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上运行并且需要使用 SQLXML 4.0 时，如果计算机上没有安装 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，则必须下载 SQLXML 4.0 SP1 并安装它。  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>在使用 SQLOLEDB 和 SQL Server Native Client OLE DB 访问接口的新数据类型时 SQLXML 4.0 SP1 的行为  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中引入了以下数据类型，使用 SQLXML 的开发人员可能需要使用这些数据类型：  
  
-   `Date`  
  
-   `Time`  
  
-   `DateTime2`  
  
-   `DateTimeOffset`  
  
 如果将 SQLXML 4.0 SP1 与 SQLOLEDB（来自 Windows 数据访问组件，以前为 Microsoft 数据访问组件）或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB（来自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]）一起使用，这些新类型将作为字符串显示给开发人员。 如果将 SQLXML 4.0 SP1 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 一起使用，SQLXML 4.0 SP1 会将这四种新数据类型作为内置标量类型来使用。 在下载 SQLXML 4.0 SP1 之前，将这些类型映射到非字符串类型可能会导致截断某些数据。 例如，映射`DateTime2`到`xsd:date`将导致数据被截断为[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] `DateTime` 3.33 毫秒的精度。  
  
## <a name="see-also"></a>请参阅  
 [SQLXML 4.0 编程概念](sqlxml-4-0-programming-concepts.md)  
  
  
