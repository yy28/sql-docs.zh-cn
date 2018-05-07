---
title: xp_msver (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_msver_TSQL
- xp_msver
dev_langs:
- TSQL
helpviewer_keywords:
- xp_msver
ms.assetid: 9264cf8c-92ba-45ad-b2d6-15d26d805a16
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: eb4961a51a7a4104fd47b64544727eb609618da4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="xpmsver-transact-sql"></a>xp_msver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关版本信息[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **xp_msver**也会返回有关服务器的实际生成号的信息和有关的服务器环境的信息。 信息的**xp_msver**返回可用于中[!INCLUDE[tsql](../../includes/tsql-md.md)]语句、 批处理、 存储的过程和等等，以增强独立于平台的代码的逻辑。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_msver [ optname ]  
```  
  
## <a name="arguments"></a>参数  
 *optname*  
 是选项名，可以是下列值之一。  
  
|选项/列名|Description|  
|-------------------------|-----------------|  
|**ProductName**|产品名称;例如， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**ProductVersion**|产品版本。|  
|**语言**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的语言版本。|  
|**平台**|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机的操作系统名称、制造商名称以及芯片系列名称。|  
|**注释**|有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的杂项信息。|  
|**CompanyName**|生产 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的公司名称，例如，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation。|  
|**FileDescription**|操作系统。|  
|**FileVersion**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可执行文件的版本。|  
|**InternalName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部名称，例如，SQLSERVR。|  
|**LegalCopyright**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所需的合法版权信息。例如，Copyright© [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corp. 1988-2005。|  
|**LegalTrademarks**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所需的合法商标信息。 例如，[!INCLUDE[msCoName](../../includes/msconame-md.md)] 是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation 的注册商标。|  
|**OriginalFilename**|启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时执行的文件名。例如，Sqlservr.exe。|  
|**PrivateBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**SpecialBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**WindowsVersion**|运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的计算机上所安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 的版本。|  
|**ProcessorCount**|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机中的处理器数目。|  
|**ProcessorActiveMask**|指示运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机中安装的、可由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 启动并使用的处理器。|  
|**ProcessorType**|处理器类型。 类似于**平台**。|  
|**物理内存**|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上安装的 RAM 的容量 (MB)。|  
|**产品 ID**|产品 ID (PID) 号。 该参数在安装时指定。 该号码印在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原始光盘盒的不干胶标签上。|  
  
## <a name="return-code-values"></a>返回代码值  
 1 （成功）  
  
## <a name="result-sets"></a>结果集  
 **xp_msver**，不带任何参数，返回四个列结果集，其中列出了所有选项值。 **xp_msver**，对于任何参数，返回的四个列结果集与该选项的值。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [常规扩展存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [@@VERSION (Transact-SQL)](../../t-sql/functions/version-transact-sql-configuration-functions.md)  
  
  
