---
title: 客户端连接中的服务主体名称 (SPN) (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ae38f4258c965a3b4aedf18ed6261134bd00ac6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62626850"
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>客户端连接中的服务主体名称 (SPN) (OLE DB)
  本主题说明支持客户端应用程序中的服务主体名称 (SPN) 的 OLE DB 属性和成员函数。 有关客户端应用程序中 SPN 的详细信息，请参阅[客户端连接中的服务主体名称 &#40;SPN&#41; 支持](../features/service-principal-name-spn-support-in-client-connections.md)。 有关示例，请参阅[集成的 Kerberos 身份验证 (OLE DB)](../../native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md)。  
  
## <a name="provider-initialization-string-keywords"></a>访问接口初始化字符串关键字  
 以下访问接口初始化字符串关键字支持 OLE DB 应用程序中的 SPN。 在下表中，关键字列中的值用于 IDBInitialize::Initialize 的访问接口字符串。 使用 ADO 或 IDataInitialize::GetDataSource 建立连接时，在初始化字符串中使用说明列中的值。  
  
|关键字|说明|值|  
|-------------|-----------------|-----------|  
|ServerSPN|服务器 SPN|服务器的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
|FailoverPartnerSPN|故障转移伙伴 SPN|故障转移伙伴的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
  
## <a name="data-source-initialization-properties"></a>数据源初始化属性  
 `DBPROPSET_SQLSERVERDBINIT` 属性集中的以下属性允许应用程序指定 SPN。  
  
|名称|类型|使用情况|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR，读/写|指定服务器的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR，读/写|指定故障转移伙伴的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
  
## <a name="data-source-properties"></a>数据源属性  
 `DBPROPSET_SQLSERVERDATASOURCEINFO` 属性集中的以下属性支持应用程序发现身份验证方法。  
  
|名称|类型|使用情况|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR，只读|返回用于连接的身份验证方法。 返回到应用程序的值是 Windows 返回到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的值。 以下列出的是可能的值：<br /><br /> -"NTLM"，在使用 NTLM 身份验证打开连接时返回。<br />-"Kerberos"，在使用 Kerberos 身份验证打开连接时返回。<br /><br /> 如果已经打开连接但无法确定身份验证方法，将返回 VT_EMPTY。<br /><br /> 只能在已经初始化数据源时读取此属性。 如果试图在初始化数据源之前读取该属性，IDBProperties::GetProperies 将视情况返回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，并且将在 DBPROPSET_PROPERTIESINERROR 中为此属性设置 DBPROPSTATUS_NOTSUPPORTED。 此行为符合 OLE DB 核心规范。|  
|SSPROP_MUTUALLYAUTHENICATED|VT_ BOOL，只读|如果建立连接的服务器之间已通过相互身份验证，则返回 VARIANT_TRUE；否则返回 VARIANT_FALSE。<br /><br /> 只能在已经初始化数据源时读取此属性。 如果试图在初始化数据源之前读取该属性，IDBProperties::GetProperies 将视情况返回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，并且将在 DBPROPSET_PROPERTIESINERROR 中为此属性设置 DBPROPSTATUS_NOTSUPPORTED。 此行为符合 OLE DB 核心规范<br /><br /> 如果针对未使用 Windows 身份验证的连接查询此属性，将返回 VARIANT_FALSE。|  
  
## <a name="ole-db-api-support-for-spns"></a>OLE DB API 对 SPN 的支持  
 下表对支持客户端连接中的 SPN 的 OLE DB 成员函数进行了说明：  
  
|成员函数|说明|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString*可以包含新的关键字`ServerSPN`和`FailoverPartnerSPN`。|  
|IDataInitialize::GetInitializationString|如果 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 具有非默认值，则这些值将通过*ppwszInitString*作为`ServerSPN`和`FailoverPartnerSPN`的关键字值包括在初始化字符串中。 如果有默认值，这些关键字将不包括在初始化字符串中。|  
|IDBInitialize::Initialize|如果通过在数据源初始化属性中设置 DBPROP_INIT_PROMPT 启用了提示功能，将显示 OLE DB“登录”对话框。 这允许为主体服务器及其故障转移伙伴输入 SPN。<br /><br /> 如果设置，DPPROP_INIT_PROVIDERSTRING 中的提供程序字符串将识别新关键字`ServerSPN`并`FailoverPartnerSPN`使用它们的值（如果存在）来初始化 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN。<br /><br /> 在调用 IDBInitialize::Initialize 之前，可以通过调用 IDBProperties::SetProperties 来设置属性 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN。 这是使用访问接口字符串的替代方法。<br /><br /> 如果在多个位置设置了某属性，以编程方式设置的值优先于在访问接口字符串中设置的值。 在初始化字符串中设置的值优先于在登录对话框中设置的值。<br /><br /> 如果同一关键字多次出现在访问接口字符串中，首次出现的值的优先级最高。|  
|IDBProperties::GetProperties|可以调用 IDBProperties::GetProperties 来获取新的数据源初始化属性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 的值，以及新的数据源属性 SSPROP_AUTHENTICATIONMETHOD 和 SSPROP_MUTUALLYAUTHENTICATED 的值。|  
|IDBProperties::GetPropertyInfo|IdbProperties::GetPropertyInfo 将包括新的数据源初始化属性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN，或者新的数据源属性 SSPROP_AUTHENTICATION_METHOD 和 SSPROP_MUTUALLYAUTHENTICATED。|  
|IDBProperties::SetProperties|可以调用 IDBProperties::SetProperties 来设置新的数据源初始化属性 SSPROP_INITSERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 的值。<br /><br /> 可以随时设置这些属性，不过如果数据源已经打开，将返回以下错误：DB_E_ERRORSOCCURRED，“多步 OLE DB 操作生成了错误。 检查每个 OLE DB 状态值（如果有）。 未执行任何操作。”|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](sql-server-native-client-ole-db.md)  
  
  
