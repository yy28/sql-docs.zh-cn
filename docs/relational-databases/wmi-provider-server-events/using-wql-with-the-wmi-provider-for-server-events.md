---
title: 将 WQL 与 WMI Provider for Server Events 结合使用
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 57f7e07de49b2591e9ab0ef74603d674543282e9
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660492"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>将 WQL 与 WMI Provider for Server Events 结合使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  管理应用程序通过发出 WMI 查询语言 (WQL) 语句来访问使用 WMI Provider for Server Events 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 WQL 是结构化查询语言 (SQL) 的简化子集，它还包含一些特定于 WMI 的扩展。 当使用 WQL 时，应用程序将针对特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例、数据库或数据库对象（当前唯一支持的对象为队列）来检索事件类型。 用于服务器事件的 WMI 提供程序将查询转换为在数据库范围内或对象范围的事件通知的目标数据库中创建的事件通知，或在用于服务器范围内的事件通知的**master**数据库中创建的事件通知。  
  
 例如，请考虑下列 WQL 查询：  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS WHERE DatabaseName = 'AdventureWorks'  
```  
  
 在以下查询中，WMI 提供程序试图在目标服务器上生成此事件通知的等效项：  
  
```  
USE AdventureWorks ;  
GO  
  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE   
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',  
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 WQL 查询 (`FROM`) 的 `DDL_DATABASE_LEVEL_EVENTS` 子句中的参数可以为可对其创建事件通知的任何有效事件。 `SELECT` 和 `WHERE` 子句中的参数可以指定与某一事件或其父事件关联的任何事件属性。 有关有效事件和事件属性的列表，请参阅[事件通知（数据库引擎）](https://technet.microsoft.com/library/ms182602.aspx)。  
  
 WMI Provider for Server Events 显式支持以下 WQL 语法。 也可以指定附加 WQL 语法，但该语法并非特定于此提供程序，并且由 WMI 主机服务进行分析。 有关 WMI 查询语言的详细信息，请参阅 Microsoft Developer Network (MSDN) 上的 WQL 文档。  
  
## <a name="syntax"></a>语法  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>参数  
 *event_property*  
 事件的属性。 示例包括**PostTime**、 **SPID**和**LoginName**。 查找[WMI Provider For Server Events 类和属性](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)中列出的每个事件，以确定其包含的属性。 例如，"DDL_DATABASE_LEVEL_EVENTS" 事件包含 " **DatabaseName** " 和 "**用户名**" 属性。 它还从其父事件继承了**SQLInstance**、 **LoginName**、 **PostTime**、 **SPID**和**ComputerName**属性。  
  
 **,** *...n*  
 指示*event_property*可以查询多次，用逗号分隔。  
  
 \*  
 指定对与事件关联的所有属性进行查询。  
  
 event_type  
 可针对其创建事件通知的任何事件。 有关可用事件的列表，请参阅[WMI Provider For Server Events 类和属性](https://technet.microsoft.com/library/ms186449.aspx)。 请注意，*事件类型*名称对应于在使用 CREATE event notification 手动创建事件通知时可以指定的相同*event_type* | *event_group* 。 *事件类型*的示例包括 CREATE_TABLE、LOCK_DEADLOCK、DDL_USER_EVENTS 和 TRC_DATABASE。  
  
> [!NOTE]  
>  执行 DDL 式操作的某些系统存储过程也可以激发事件通知。 测试您的事件通知以确定它们是否响应运行的系统存储过程。 例如，CREATE TYPE 语句和**sp_addtype**存储过程都将激发在 CREATE_TYPE 事件上创建的事件通知。 但**sp_rename**存储过程不会激发任何事件通知。 有关详细信息，请参阅[DDL 事件](../../relational-databases/triggers/ddl-events.md)。  
  
 *where_condition*  
 一个 WHERE 子句查询谓词，其中包含*event_property*名称和逻辑运算符和比较运算符。 *Where_condition*确定在目标数据库中注册相应事件通知的范围。 它还可以充当筛选器，以面向要从中查询 event_type 的特定架构或对象 *。* 有关详细信息，请参阅本主题后面的 "备注" 部分。  
  
 只能将 `=` 操作数与**DatabaseName**、 **SchemaName**和**ObjectName**一起使用。 其他表达式不能与这些事件属性一起使用。  
  
## <a name="remarks"></a>注释  
 "用于服务器事件的 WMI 提供程序" 语法的*where_condition*确定以下各项：  
  
-   提供程序尝试检索指定*event_type*的作用域：服务器级别、数据库级别或对象级别（当前唯一支持的对象是队列）。 最后，此范围用于确定在目标数据库中创建的事件通知的类型。 这个过程称为事件通知注册。  
  
-   要在其上进行注册的数据库、架构和对象（视具体情况而定）。  
  
 WMI Provider for Server Events 使用从下到上的最先适应算法为基础 EVENT NOTIFICATION 生成尽可能小的范围。 该算法试图将服务器上的内部活动和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例与 WMI 主机进程之间的网络通信流量降至最低。 提供程序检查 FROM 子句中指定的*event_type*和 WHERE 子句中的条件，并尝试向最小的可能范围注册基础事件通知。 如果提供程序无法在最小的范围内注册，则它会依次尝试在更大的范围内注册，直到注册最终成功为止。 如果它达到服务器级别的最大范围且失败，则它将向使用者返回一个错误。  
  
 例如，如果在 WHERE 子句中指定 DatabaseName = **'** AdventureWorks **'** ，则提供程序将尝试在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中注册事件通知。 如果 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库存在且调用客户端拥有在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中创建事件通知所需的权限，则注册成功。 否则，将尝试在服务器级别注册事件通知。 如果 WMI 客户端拥有所需的权限，则注册成功。 但是，在这种情况下，在创建完 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库之前不会将事件返回给客户端。  
  
 *Where_condition*还可以充当筛选器，以进一步限制特定数据库、架构或对象的查询。 例如，请考虑下列 WQL 查询：  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 根据注册过程的结果的不同，可以在数据库级别或服务器级别注册此 WQL 查询。 但是，即使此查询的注册是在服务器级别进行的，提供程序最终还是会筛选不适用于 `ALTER_TABLE` 表的所有 `AdventureWorks.Sales.SalesOrderDetail` 事件。 也就是说，提供程序只会返回在此特定表上出现的 `ALTER_TABLE` 事件的属性。  
  
 如果指定复合表达式，例如 `DatabaseName='AW1'` OR `DatabaseName='AW2'`，则会尝试在服务器范围注册单个事件通知，而不是两个独立的事件通知。 如果调用客户端拥有权限，则注册成功。  
  
 如果 `WHERE` 子句中指定了 `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'`，则尝试直接在架构 `X`中的对象 `Z` 上注册事件通知。 如果客户端拥有权限，则注册成功。 请注意，当前仅在队列上支持对象级事件，并且仅针对 QUEUE_ACTIVATION *event_type*。  
  
 请注意，并非所有事件均可在任何特定的范围内进行查询。 例如，针对跟踪事件（例如 Lock_Deadlock）或跟踪事件组（例如 TRC_LOCKS）的 WQL 查询仅可在服务器级别进行注册。 与此类似，CREATE_ENDPOINT 事件和 DDL_ENDPOINT_EVENTS 事件组也只能在服务器级别进行注册。 有关用于注册事件的适当范围的详细信息，请参阅[设计事件通知](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx)。 尝试注册 WQL 查询（其*event_type*只能在服务器级别注册）始终在服务器级别进行。 如果 WMI 客户端拥有权限，则注册成功。 否则，将向客户端返回一个错误。 不过，在某些情况下，仍可根据与服务器级别事件对应的属性将 WHERE 子句用作服务器级别事件的筛选器。 例如，许多跟踪事件都有一个**DatabaseName**属性，该属性可在 WHERE 子句中用作筛选器。  
  
 服务器范围内的事件通知在**master**数据库中创建，并且可以通过使用[sys. server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)目录视图来查询元数据。  
  
 数据库范围内或对象范围内的事件通知在指定的数据库中创建，并且可以通过使用[sys. event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)目录视图来查询元数据。 （您必须为目录视图加上对应的数据库名前缀。）  
  
## <a name="examples"></a>示例  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>A. 在服务器范围查询事件  
 以下 WQL 查询检索在 `SERVER_MEMORY_CHANGE` 实例上出现的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 跟踪事件的所有事件属性。  
  
```  
SELECT * FROM SERVER_MEMORY_CHANGE  
```  
  
### <a name="b-querying-for-events-at-the-database-scope"></a>B. 在数据库范围查询事件  
 以下 WQL 查询检索在 `AdventureWorks` 数据库中出现且存在于 `DDL_DATABASE_LEVEL_EVENTS` 事件组下的任何事件的特定事件属性。  
  
```  
SELECT SPID, SQLInstance, DatabaseName FROM DDL_DATABASE_LEVEL_EVENTS   
WHERE DatabaseName = 'AdventureWorks'   
```  
  
### <a name="c-querying-for-events-at-the-database-scope-filtering-by-schema-and-object"></a>C. 在数据库范围查询事件，并按架构和对象进行筛选  
 以下查询检索在表 `ALTER_TABLE` 上出现的任何 `AdventureWorks.Sales.SalesOrderDetail` 事件的所有事件属性。  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
## <a name="see-also"></a>另请参阅  
 [WMI Provider For Server Events 的概念](https://technet.microsoft.com/library/ms180560.aspx)   
 [事件通知（数据库引擎）](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
