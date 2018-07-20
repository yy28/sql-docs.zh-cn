---
title: 系统基表 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6804649b60a1617def415ce35113685ef43902f5
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102205"
---
# <a name="system-base-tables"></a>系统基表
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  系统基表是基础表，用于实际存储特定数据库的元数据。 **主**数据库是在这一方面特殊，因为它包含在任何其他数据库中找不到某些其他表。 这些表包含服务器范围内的持久化元数据。  
  
> [!IMPORTANT]  
>  系统基表仅在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]内使用，并且不能用于一般客户。 随时可能对其进行更改，不保证兼容性。  
  
## <a name="system-base-table-metadata"></a>系统基表元数据  
 对数据库具有 CONTROL、 ALTER 或 VIEW DEFINITION 权限的被授权者可以查看系统基表元数据**sys.objects**目录视图。 被授权者还可以解析的名称，并使用内置函数类似于对象 Id 的系统基表[OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md)并[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)。  
  
 若要绑定到系统基表，用户必须通过使用专用管理员连接 (DAC) 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 如果在没有使用 DAC 进行连接的情况下尝试从系统基表执行 SELECT 查询，则会引发错误。  
  
> [!IMPORTANT]  
>  通过使用 DAC 访问系统基表的功能是专门为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 人员设计的，它不是支持的客户方案。  
  
## <a name="system-base-tables"></a>系统基表  
 下表列出并描述了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的每个系统基表。  
  
|基表|Description|  
|----------------|-----------------|  
|**sys.sysschobjs**|存在于每个数据库中。 每一行表示数据库中的一个对象。|  
|**sys.sysbinobjs**|存在于每个数据库中。 数据库中的每个 Service Broker 实体都存在对应的一行。 Service Broker 实体包括以下内容：<br /><br /> 消息类型<br /><br /> 服务约定<br /><br /> 服务<br /><br /> 名称和类型使用固定的二进制排序规则。|  
|**sys.sysclsobjs**|存在于每个数据库中。 共享相同通用属性的每个分类实体均存在对应的一行，这些属性包括以下内容：<br /><br /> Assembly<br /><br /> 备份设备<br /><br /> 全文目录<br /><br /> 分区函数<br /><br /> 分区方案<br /><br /> 文件组<br /><br /> 模糊处理键|  
|**sys.sysnsobjs**|存在于每个数据库中。 每个命名空间范围内的实体均存在对应的一行。 此表用于存储 XML 集合实体。|  
|**sys.syscolpars**|存在于每个数据库中。 表、视图或表值函数的每个列均存在对应的一行。 过程或函数的每个参数也存在对应的行。|  
|**sys.systypedsubobjs**|存在于每个数据库中。 每个类型化的子实体均存在对应的一行。 只有分区函数的参数属于此类别。|  
|**sys.sysidxstats**|存在于每个数据库中。 表和索引视图的每个索引或统计信息均存在对应的一行<br /><br /> 注意： 每个索引 （除了堆） 是与具有相同的名称作为索引的统计信息相关联。|  
|**sys.sysiscols**|存在于每个数据库中。 每个持久化索引和统计信息列均存在对应的一行。|  
|**sys.sysscalartypes**|存在于每个数据库中。 每个用户定义类型或系统类型均存在对应的一行。|  
|**sys.sysdbreg**|中存在**主**仅数据库。 每个注册数据库均存在对应的一行。|  
|**sys.sysxsrvs**|中存在**主**仅数据库。 每个本地服务器、链接服务器或远程服务器均存在对应的一行。|  
|**sys.sysrmtlgns**|此系统基表中存在**主**仅数据库。 每个远程登录映射均存在对应的一行。 这用于将声明来自对应服务器的传入登录映射到实际本地登录。|  
|**sys.syslnklgns**|中存在**主**仅数据库。 每个链接登录映射均存在对应的一行。 链接登录映射由远程过程调用和分布式查询使用，从本地服务器发出到对应的链接服务器。|  
|**sys.sysxlgns**|中存在**主**仅数据库。 每个服务器主体均存在对应的一行。|  
|**sys.sysdbfiles**|存在于每个数据库中。 如果该列**dbid**为零，则该行表示一个属于此数据库的文件。 在中**主**数据库中，列**dbid**可以为非零值。 如果是这样，该行表示主文件。|  
|**sys.sysusermsg**|中存在**主**仅数据库。 每一行表示用户定义的错误消息。|  
|**sys.sysprivs**|存在于每个数据库中。 每个数据库或服务器级权限均存在对应的一行。<br /><br /> 注意： 服务器级权限存储在**主**数据库。|  
|**sys.sysowners**|存在于每个数据库中。 每一行表示一个数据库主体。|  
|**sys.sysobjkeycrypts**|存在于每个数据库中。 每个与对象关联的对称密钥、加密或加密属性均存在对应的一行。|  
|**sys.syscerts**|存在于每个数据库中。 数据库中的每个证书均存在对应的一行。|  
|**sys.sysasymkeys**|存在于每个数据库中。 每一行表示一个非对称密钥。|  
|**sys.ftinds**|存在于每个数据库中。 数据库中的每个全文索引均存在对应的一行。|  
|**sys.sysxprops**|存在于每个数据库中。 每个扩展属性均存在对应的一行。|  
|**sys.sysallocunits**|存在于每个数据库中。 每个存储分配单元均存在对应的一行。|  
|**sys.sysrowsets**|存在于每个数据库中。 索引或堆的每个分区行集均存在对应的一行。|  
|**sys.sysrowsetrefs**|存在于每个数据库中。 行集引用的每个索引均存在对应的一行。|  
|**sys.syslogshippers**|中存在**主**仅数据库。 每个数据库镜像见证服务器均存在对应的一行。|  
|**sys.sysremsvcbinds**|存在于每个数据库中。 每个远程服务绑定均存在对应的一行。|  
|**sys.sysconvgroup**|存在于每个数据库中。 Service Broker 中的每个服务实例均存在对应的一行。|  
|**sys.sysxmitqueue**|存在于每个数据库中。 每个 Service Broker 传输队列均存在对应的一行。|  
|**sys.sysdesend**|存在于每个数据库中。 Service Broker 会话的每个发送端点均存在对应的一行。|  
|**sys.sysdercv**|存在于每个数据库中。 Service Broker 会话的每个接收端点均存在对应的一行。|  
|**sys.sysendpts**|中存在**主**仅数据库。 服务器中创建的每个端点均存在对应的一行。|  
|**sys.syswebmethods**|中存在**主**仅数据库。 对服务器中创建的启用 SOAP 的 HTTP 端点定义的每个 SOAP 方法均存在对应的一行。|  
|**sys.sysqnames**|存在于每个数据库中。 4 字节 ID 标记的每个命名空间或限定名均存在对应的一行。|  
|**sys.sysxmlcomponent**|存在于每个数据库中。 每一行表示一个 XML 架构组件。|  
|**sys.sysxmlfacet**|存在于每个数据库中。 具有 XML 类型定义的每个 XML 方面（限制）均存在对应的一行。|  
|**sys.sysxmlplacement**|存在于每个数据库中。 XML 组件的每个 XML 位置均存在对应的一行。|  
|**sys.syssingleobjrefs**|存在于每个数据库中。 每个常规 N 到 1 引用均存在对应的一行。|  
|**sys.sysmultiobjrefs**|存在于每个数据库中。 每个常规 N 到 N 引用均存在对应的一行。|  
|**sys.sysobjvalues**|存在于每个数据库中。 实体的每个常规值属性均存在对应的一行。|  
|**sys.sysguidrefs**|存在于每个数据库中。 每个 GUID 分类 ID 引用均存在对应的一行。|  
  
  
