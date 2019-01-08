---
title: 配置事件通知的对话安全设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c62812b138afef0244bbad5f3d17bafb4064537
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359519"
---
# <a name="configure-dialog-security-for-event-notifications"></a>配置事件通知的对话安全模式
  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话安全模式。 必须按照 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 对话完全安全模式手动配置对话安全模式。 完全安全模式可以为在远程服务器之间发送的消息启用加密和解密功能。 虽然事件通知单向发送，但其他消息（例如错误）也会从相反的方向返回。  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>配置事件通知的对话安全模式  
 下面的步骤中介绍了针对事件通知实现对话安全模式所需的步骤。 这些步骤包括同时在源服务器和目标服务器中执行的操作。 源服务器是创建事件通知的服务器。 目标服务器是接收事件通知消息的服务器。 在继续执行下一个步骤之前，必须针对源服务器和目标服务器完成每一个步骤中的操作。  
  
> [!IMPORTANT]  
>  所有证书的创建都必须使用有效的开始日期和过期日期。  
  
 **第 1 步：建立 TCP 端口号和目标服务名称。**  
  
 建立源服务器和目标服务器接收消息所用的 TCP 端口。 同时，必须确定目标服务的名称。  
  
 **步骤 2:配置加密和证书共享数据库级身份验证。**  
  
 同时在源服务器和目标服务器中完成下列操作。  
  
|源服务器|目标服务器|  
|-------------------|-------------------|  
|选择或创建一个数据库以包含事件通知和主密钥。|选择或创建一个数据库以包含主密钥。|  
|如果没有用于源数据库的主密钥，则 [创建主密钥](/sql/t-sql/statements/create-master-key-transact-sql)。 源数据库和目标数据库都需要主密钥来保护它们各自的证书。|如果没有用于目标数据库的主密钥，则创建主密钥。|  
|为源数据库[创建登录名](/sql/t-sql/statements/create-login-transact-sql) 和相应的 [用户](/sql/t-sql/statements/create-user-transact-sql) 。|为目标数据库创建登录名和相应的用户。|  
|为源数据库的用户[创建证书](/sql/t-sql/statements/create-certificate-transact-sql) 。|创建属于目标数据库的用户的证书。|  
|在目标服务器可以访问的文件中[备份证书](/sql/t-sql/statements/backup-certificate-transact-sql) 。|将证书备份到可以由源服务器访问的文件。|  
|[创建用户](/sql/t-sql/statements/create-user-transact-sql)，指定目标数据库的用户和 WITHOUT LOGIN。 此用户将拥有要通过备份文件创建的目标数据库证书。 用户不必映射到登录名，因为此用户的唯一目的是拥有在下面的步骤 3 中创建的目标数据库证书。|创建用户，指定源数据库的用户和 WITHOUT LOGIN。 此用户将拥有要通过备份文件创建的源数据库证书。 用户不必映射到登录名，因为此用户的唯一目的是拥有在下面的步骤 3 中创建的源数据库证书。|  
  
 **步骤 3:共享证书并授予数据库级身份验证的权限。**  
  
 同时在源服务器和目标服务器中完成下列操作。  
  
|源服务器|目标服务器|  
|-------------------|-------------------|  
|通过目标证书的备份文件[创建证书](/sql/t-sql/statements/create-certificate-transact-sql) ，将目标数据库用户指定为所有者。|通过源证书的备份文件创建证书，将源数据库用户指定为所有者。|  
|向源数据库用户[授予权限](/sql/t-sql/statements/grant-transact-sql) 以创建事件通知。 有关此权限的详细信息，请参阅 [CREATE EVENT NOTIFICATION (Transact-SQL)](/sql/t-sql/statements/create-event-notification-transact-sql)。|向目标数据库用户授予对现有事件通知 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 的 REFERENCES 权限，请访问 `https://schemas.microsoft.com/SQL/Notifications/PostEventNotification`。|  
|为目标服务[创建远程服务绑定](/sql/t-sql/statements/create-remote-service-binding-transact-sql) 并指定目标数据库用户的凭据。 远程服务绑定可以保证，源数据库用户所拥有的证书中的公钥将验证发送到目标服务器的消息。|向目标数据库用户[授予](/sql/t-sql/statements/grant-transact-sql) CREATE QUEUE、CREATE SERVICE 和 CREATE SCHEMA 权限。|  
||如果仍未以目标数据库用户身份连接到数据库，则立即执行此操作。|  
||[创建队列](/sql/t-sql/statements/create-queue-transact-sql) 以接收事件通知消息，并 [创建服务](/sql/t-sql/statements/create-service-transact-sql) 以传递消息。|  
||向源数据库用户[授予 SEND 权限](/sql/t-sql/statements/grant-transact-sql) ，此权限将针对目标服务。|  
|向目标服务器提供源数据库的 Service Broker 标识符。 此标识符可以通过查询 **sys.databases** 目录视图的 [service_broker_guid](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 列而获得。 对于服务器级事件通知，请使用 **msdb**的 Service Broker 标识符。|向源服务器提供目标数据库的 Service Broker 标识符。|  
  
 **步骤 4:创建路由并设置服务器级身份验证。**  
  
 同时在源服务器和目标服务器中完成下列操作。  
  
|源服务器|目标服务器|  
|-------------------|-------------------|  
|为目标服务[创建路由](/sql/t-sql/statements/create-route-transact-sql) ，并指定目标数据库的 Service Broker 标识符和一致的 TCP 端口号。|创建到源服务的路由，并指定源数据库的 Service Broker 标识符和一致的 TCP 端口号。 若要指定源服务，请使用下面提供的服务： `https://schemas.microsoft.com/SQL/Notifications/EventNotificationService`。|  
|切换到 **master** 数据库以配置服务器级身份验证。|切换到 **master** 数据库以配置服务器级身份验证。|  
|如果没有用于 **master** 数据库的主密钥，则 [创建主密钥](/sql/t-sql/statements/create-master-key-transact-sql)。|如果没有用于 **master** 数据库的主密钥，则创建主密钥。|  
|[创建证书](/sql/t-sql/statements/create-certificate-transact-sql) ，以对数据库进行身份验证。|创建证书，以对数据库进行身份验证。|  
|在目标服务器可以访问的文件中[备份证书](/sql/t-sql/statements/backup-certificate-transact-sql) 。|将证书备份到可以由源服务器访问的文件。|  
|[创建端点](/sql/t-sql/statements/create-endpoint-transact-sql)，并指定一致的 TCP 端口号 FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *certificate_name*) 和身份验证证书的名称。|创建端点，并指定一致的 TCP 端口号 FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *certificate_name*) 和身份验证证书的名称。|  
|[创建登录名](/sql/t-sql/statements/create-login-transact-sql)，并指定目标服务器的登录名。|创建登录名，并指定源服务器的登录名。|  
|向目标验证器登录名[授予 CONNECT 权限](/sql/t-sql/statements/grant-transact-sql) ，此权限针对端点。|向源验证器登录名授予对端点的 CONNECT 权限。|  
|[创建用户](/sql/t-sql/statements/create-user-transact-sql)，并指定目标验证器登录名。|创建用户，并指定源验证器登录名。|  
  
 **步骤 5:共享服务器级身份验证证书并创建事件通知。**  
  
 同时在源服务器和目标服务器中完成下列操作。  
  
|源服务器|目标服务器|  
|-------------------|-------------------|  
|通过目标证书的备份文件[创建证书](/sql/t-sql/statements/create-certificate-transact-sql) ，将目标验证器用户指定为所有者。|通过源证书的备份文件创建证书，将源验证器用户指定为所有者。|  
|切换到在其中创建事件通知的源数据库，如果仍未以源数据库用户身份连接，则立即执行此操作。|切换到目标数据库以接收事件通知消息。|  
|[创建事件通知](/sql/t-sql/statements/create-event-notification-transact-sql)，并指定目标数据库的 Broker Service 和标识符。||  
  
## <a name="see-also"></a>请参阅  
 [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)   
 [BACKUP CERTIFICATE (Transact-SQL)](/sql/t-sql/statements/backup-certificate-transact-sql)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [加密层次结构](../security/encryption/encryption-hierarchy.md)   
 [实现事件通知](event-notifications.md)   
 [CREATE MASTER KEY (Transact-SQL)](/sql/t-sql/statements/create-master-key-transact-sql)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE CERTIFICATE (Transact-SQL)](/sql/t-sql/statements/create-certificate-transact-sql)   
 [CREATE REMOTE SERVICE BINDING (Transact-SQL)](/sql/t-sql/statements/create-remote-service-binding-transact-sql)   
 [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)   
 [CREATE ROUTE (Transact SQL)](/sql/t-sql/statements/create-route-transact-sql)   
 [CREATE QUEUE (Transact SQL)](/sql/t-sql/statements/create-queue-transact-sql)   
 [CREATE SERVICE (Transact SQL)](/sql/t-sql/statements/create-service-transact-sql)   
 [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [CREATE EVENT NOTIFICATION (Transact-SQL)](/sql/t-sql/statements/create-event-notification-transact-sql)  
  
  
