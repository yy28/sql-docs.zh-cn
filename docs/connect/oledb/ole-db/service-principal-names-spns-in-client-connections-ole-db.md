---
title: 客户端连接 (OLE DB) 中的服务主体名称 (Spn) |Microsoft 文档
description: 客户端连接 (OLE DB) 中的服务主体名称 (Spn)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b03f6f44cd23679e3b60ce03410a9582020d84ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>客户端连接中的服务主体名称 (SPN) (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


  本主题说明支持客户端应用程序中的服务主体名称 (SPN) 的 OLE DB 属性和成员函数。 在客户端应用程序 Spn 的详细信息，请参阅[服务主体名称&#40;SPN&#41;中客户端连接支持](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)。 有关示例，请参阅[集成 Kerberos 身份验证&#40;OLE DB&#41;](../../oledb/ole-db-how-to/integrated-kerberos-authentication-ole-db.md)。  
  
## <a name="provider-initialization-string-keywords"></a>访问接口初始化字符串关键字  
 以下访问接口初始化字符串关键字支持 OLE DB 应用程序中的 SPN。 在以下表中，关键字列中的值用于 idbinitialize:: Initialize 的提供程序字符串。 使用 ADO 或 IDataInitialize::GetDataSource 进行连接时，说明列中的值是在初始化字符串中使用。  
  
|关键字|Description|“值”|  
|-------------|-----------------|-----------|  
|ServerSPN|服务器 SPN|服务器的 SPN。 默认值为空字符串，它将导致 OLE DB 驱动程序的 SQL Server 以使用默认值，提供程序生成 SPN。|  
|FailoverPartnerSPN|故障转移伙伴 SPN|故障转移伙伴的 SPN。 默认值为空字符串，它将导致 OLE DB 驱动程序的 SQL Server 以使用默认值，提供程序生成 SPN。|  
  
## <a name="data-source-initialization-properties"></a>数据源初始化属性  
 中的下列属性**dbpropset_sqlserverdbinit 限**属性集允许应用程序指定 Spn。  
  
|名称|类型|用法|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR，读/写|指定服务器的 SPN。 默认值为空字符串，它将导致 OLE DB 驱动程序的 SQL Server 以使用默认值，提供程序生成 SPN。|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR，读/写|指定故障转移伙伴的 SPN。 默认值为空字符串，它将导致 OLE DB 驱动程序的 SQL Server 以使用默认值，提供程序生成 SPN。|  
  
## <a name="data-source-properties"></a>数据源属性  
 中的下列属性**DBPROPSET_SQLSERVERDATASOURCEINFO**属性集允许应用程序能够发现的身份验证方法。  
  
|名称|类型|用法|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR，只读|返回用于连接的身份验证方法。 返回到应用程序的值是为 SQL Server，Windows 返回到 OLE DB 驱动程序的值。 以下列出的是可能的值： <br />“NTLM”，使用 NTLM 身份验证打开连接时将返回该值。<br />“Kerberos”，使用 Kerberos 身份验证打开连接时将返回该值。<br /><br /> 如果已经打开连接但无法确定身份验证方法，将返回 VT_EMPTY。<br /><br /> 只能在已经初始化数据源时读取此属性。 如果你尝试在初始化数据源之前读取属性，IDBProperties::GetProperies 将返回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，视情况而定，并将在 DBPROPSET_PROPERTIESINERROR 中设置 DBPROPSTATUS_NOTSUPPORTED此属性。 此行为符合 OLE DB 核心规范。|  
|SSPROP_MUTUALLYAUTHENICATED|VT_ BOOL，只读|如果建立连接的服务器之间已通过相互身份验证，则返回 VARIANT_TRUE；否则返回 VARIANT_FALSE。<br /><br /> 只能在已经初始化数据源时读取此属性。 如果之前已初始化的数据源读取属性的尝试，IDBProperties::GetProperies 将返回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，视情况而定且 DBPROPSTATUS_NOTSUPPORTED 将设置在 DBPROPSET_此属性的 PROPERTIESINERROR。 此行为是根据 OLE DB 核心规范<br /><br /> 如果针对未使用 Windows 身份验证的连接查询此属性，将返回 VARIANT_FALSE。|  
  
## <a name="ole-db-api-support-for-spns"></a>OLE DB API 对 SPN 的支持  
 下表对支持客户端连接中的 SPN 的 OLE DB 成员函数进行了说明：  
  
|成员函数|Description|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString*可以包含新关键字**ServerSPN**和**FailoverPartnerSPN**。|  
|IDataInitialize::GetInitializationString|如果 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 具有非默认值，它们将包含在初始化字符串通过*ppwszInitString*作为的关键字值**ServerSPN**和**FailoverPartnerSPN**。 如果有默认值，这些关键字将不包括在初始化字符串中。|  
|IDBInitialize::Initialize|如果通过在数据源初始化属性中设置 DBPROP_INIT_PROMPT 启用了提示功能，将显示 OLE DB“登录”对话框。 这允许为主体服务器及其故障转移伙伴输入 SPN。<br /><br /> 提供程序字符串在 DPPROP_INIT_PROVIDERSTRING，如果设置，将识别新关键字**ServerSPN**和**FailoverPartnerSPN**并使用它们的值，如果存在，初始化 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN。<br /><br /> 可以调用 IDBProperties::SetProperties 调用 idbinitialize:: Initialize 之前设置 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN 的属性。 这是使用访问接口字符串的替代方法。<br /><br /> 如果在多个位置设置了某属性，以编程方式设置的值优先于在访问接口字符串中设置的值。 在初始化字符串中设置的值优先于在登录对话框中设置的值。<br /><br /> 如果同一关键字多次出现在访问接口字符串中，首次出现的值的优先级最高。|  
|IDBProperties::GetProperties|可以调用 IDBProperties::GetProperties 以获取值的新数据源初始化属性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN，和的新数据源属性 SSPROP_AUTHENTICATIONMETHOD 和 SSPROP_MUTUALLYAUTHENTICATED。|  
|IDBProperties::GetPropertyInfo|IdbProperties::GetPropertyInfo 将包括新数据源初始化属性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 或新的数据源属性 SSPROP_AUTHENTICATION_METHOD 和 SSPROP_MUTUALLYAUTHENTICATED。|  
|IDBProperties::SetProperties|可以调用 IDBProperties::SetProperties 设置 SSPROP_INITSERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 初始化属性的新数据源的值。<br /><br /> 可以随时设置这些属性，不过如果数据源已经打开，将返回以下错误：DB_E_ERRORSOCCURRED，“多步 OLE DB 操作生成了错误。 检查每个 OLE DB 状态值（如果有）。 未执行任何操作。”|  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
