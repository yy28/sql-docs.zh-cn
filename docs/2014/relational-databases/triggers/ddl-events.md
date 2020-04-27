---
title: DDL 事件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c9c90dbb072ace600258edfb4ff13f99ecadf188
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68196517"
---
# <a name="ddl-events"></a>DDL 事件
  下表列出了可用于激发 DDL 触发器或事件通知的 DDL 事件。 注意，每个事件都对应于一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或存储过程，并且语句语法修改为在关键字之间加入了一个下划线字符 (_)。  
  
> [!IMPORTANT]  
>  执行类似 DDL 的操作的系统存储过程也可以激发 DDL 触发器和事件通知。 请测试您的 DDL 触发器和事件通知以确定它们是否响应运行的系统存储过程。 例如，CREATE TYPE 语句和 **sp_addtype** 存储过程都将激发针对 CREATE_TYPE 事件创建的 DDL 触发器或事件通知。  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>具有服务器或数据库作用域的 DDL 语句  
 可以创建 DDL 触发器或事件通知，以便在其中创建了它们的数据库发生以下事件（或服务器实例中的任何位置发生以下事件时）激发它们以做出响应。  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE（适用于 CREATE APPLICATION ROLE 语句和 **sp_addapprole**。 如果创建新架构，则此事件还会触发 CREATE_SCHEMA 事件）。|ALTER_APPLICATION_ROLE（适用于 ALTER APPLICATION ROLE 语句和 **sp_approlepassword**）。|DROP_APPLICATION_ROLE（适用于 DROP APPLICATION ROLE 语句和 **sp_dropapprole**）。|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE（当指定 ON DATABASE 时，适用于 ALTER AUTHORIZATION 语句和 **sp_changedbowner**。）||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPEFICIATION|ALTER_DATABASE_AUDIT_SPEFICIATION|DENY_DATABASE_AUDIT_SPEFICIATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT（适用于 **sp_bindefault**。）|UNBIND_DEFAULT（适用于 **sp_unbindefault**。）||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY（适用于 **sp_addextendedproperty**。）|ALTER_EXTENDED_PROPERTY（适用于 **sp_updateextendedproperty**。）|DROP_EXTENDED_PROPERTY（适用于 **sp_dropextendedproperty**。）|  
|CREATE_FULLTEXT_CATALOG（当指定 create  时适用于 CREATE FULLTEXT CATALOG 语句和 *sp_fulltextcatalog*。）|ALTER_FULLTEXT_CATALOG（当指定  start_incremental、  start_full、  Stop 或  Rebuild 时，适用于 ALTER FULLTEXT CATALOG 语句 *sp_fulltextcatalog*，当指定  enable 时，适用于 *sp_fulltext_database*。）|DROP_FULLTEXT_CATALOG（当指定  drop 时，适用于 DROP FULLTEXT CATALOG 语句和 *sp_fulltextcatalog*。）|  
|CREATE_FULLTEXT_INDEX（当指定  create 时，适用于 CREATE FULLTEXT INDEX 语句和 *sp_fulltexttable*。）|ALTER_FULLTEXT_INDEX（当指定 start_full   、start_incremental 或  stop 时，适用于 ALTER FULLTEXT INDEX 语句和 *sp_fulltextcatalog*，当指定除了 create  或  drop 操作之外时，适用于 *sp_fulltext_column* 和 *sp_fulltext_table*。）|DROP_FULLTEXT_INDEX（当指定  drop 时，适用于 DROP FULLTEXT INDEX 语句和 *sp_fulltexttable*。）|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX（适用于ALTER INDEX 语句和 **sp_indexoption**。）|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE（适用于 **sp_create_plan_guide**。）|ALTER_PLAN_GUIDE（当指定 ENABLE、ENABLE ALL、DISABLE 或 DISABLE ALL 时适用于 **sp_control_plan_guide** 。）|DROP_PLAN_GUIDE（当指定 DROP 或 DROP ALL 时适用于 **sp_control_plan_guide** 。）|  
|CREATE_PROCEDURE|ALTER_PROCEDURE（适用于 ALTER PROCEDURE 语句和 **sp_procoption**。）|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME（适用于 **sp_rename**）|||  
|CREATE_ROLE（适用于 CREATE ROLE 语句、 **sp_addrole**和 **sp_addgroup**。）|ALTER_ROLE|DROP_ROLE（适用于 DROP ROLE 语句、 **sp_droprole**和 **sp_dropgroup**。）|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE（适用于 **sp_bindrule**。）|UNBIND_RULE（适用于 **sp_unbindrule**。）||  
|CREATE_SCHEMA（适用于 CREATE SCHEMA 语句、**sp_addrole** **sp_adduser**、**sp_addgroup** 和 **sp_grantdbaccess**。）|ALTER_SCHEMA（适用于 ALTER SCHEMA 语句和 **sp_changeobjectowner**）。|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE（用于对非架构范围的对象的签名操作；数据库，程序集，触发器）|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT（用于架构范围的对象；存储过程，函数）|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX 可用于空间索引。|DROP_INDEX 可用于空间索引。|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE（适用于 ALTER TABLE 语句和 **sp_tableoption**。）|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER（适用于 ALTER TRIGGER 语句和 **sp_settriggerorder**。）|DROP_TRIGGER|  
|CREATE_TYPE（适用于 CREATE TYPE 语句和 **sp_addtype**）|DROP_TYPE（适用于 DROP TYPE 语句和 **sp_droptype**。）||  
|CREATE_USER（适用于 CREATE USER 语句、 **sp_adduser**和 **sp_grantdbaccess**）|ALTER_USER（应用于 ALTER USER 语句和 **sp_change_users_login**。）|DROP_USER（适用于 DROP USER 语句、 **sp_dropuser**和 **sp_revokedbaccess**。）|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX 可用于 XML 索引。|DROP_INDEX 可用于 XML 索引。|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>具有服务器作用域的 DDL 语句  
 可以创建当服务器实例中的任何位置发生以下事件时被激发以响应这些事件的 DDL 触发器或事件通知。  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE（当指定了本地服务器实例时，适用于 **sp_configure** 和 **sp_addserver** 。）|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE（适用于 ALTER DATABASE 语句和 **sp_fulltext_database**。）|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE（适用于 **sp_addextendedproc**。）|DROP_EXTENDED_PROCEDURE（适用于 **sp_dropextendedproc**。）||  
|CREATE_LINKED_SERVER（适用于 **sp_addlinkedserver**。）|ALTER_LINKED_SERVER（适用于 **sp_serveroption**。）|DROP_LINKED_SERVER（当指定了链接服务器时，适用于 **sp_dropserver** 。）|  
|CREATE_LINKED_SERVER_LOGIN（适用于 **sp_addlinkedsrvlogin**。）|DROP_LINKED_SERVER_LOGIN（适用于 **sp_droplinkedsrvlogin**。）||  
|CREATE_LOGIN（当使用必须隐式创建的不存在登录名时，适用于 CREATE LOGIN 语句、**sp_addlogin** **sp_grantlogin** **xp_grantlogin** 和 **sp_denylogin**。）|ALTER_LOGIN（当指定  Auto_Fix 时，适用于**sp_defaultdb**、**sp_defaultlanguage**、**sp_password** 和 *sp_change_users_login*。）|DROP_LOGIN（适用于 DROP LOGIN 语句、 **sp_droplogin**、 **sp_revokelogin**和 **xp_revokelogin**）|  
|CREATE_MESSAGE（适用于 **sp_addmessage**。）|ALTER_MESSAGE（适用于 **sp_altermessage**。）|DROP_MESSAGE（适用于 **sp_dropmessage**。）|  
|CREATE_REMOTE_SERVER（适用于 **sp_addserver**。）|ALTER_REMOTE_SERVER（适用于 **sp_setnetname**。）|DROP_REMOTE_SERVER（当指定了远程服务器时，适用于 **sp_dropserver** 。）|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>另请参阅  
 [DDL 触发器](ddl-triggers.md)   
 [事件通知](../service-broker/event-notifications.md)   
 [DDL 事件组](ddl-event-groups.md)  
  
  
