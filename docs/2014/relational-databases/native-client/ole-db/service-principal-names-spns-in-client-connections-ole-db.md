---
title: 客户端连接 (OLE DB) 中的服务主体名称 (Spn) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28a18050d90f04195396bf4f121719823b18282f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421756"
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>客户端连接中的服务主体名称 (SPN) (OLE DB)
  本主题说明支持客户端应用程序中的服务主体名称 (SPN) 的 OLE DB 属性和成员函数。 在客户端应用程序中的 Spn 的详细信息，请参阅[服务主体名称&#40;SPN&#41;中的客户端连接支持](../features/service-principal-name-spn-support-in-client-connections.md)。 有关示例，请参阅[集成的 Kerberos 身份验证&#40;OLE DB&#41;](../../native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md)。  
  
## <a name="provider-initialization-string-keywords"></a>访问接口初始化字符串关键字  
 以下访问接口初始化字符串关键字支持 OLE DB 应用程序中的 SPN。 在下表中，关键字列中的值用于 idbinitialize:: Initialize 的提供程序字符串。 使用 ADO 或 idatainitialize:: Getdatasource 进行连接时，是在初始化字符串中使用说明列中的值。  
  
|关键字|Description|ReplTest1|  
|-------------|-----------------|-----------|  
|ServerSPN|服务器 SPN|服务器的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
|FailoverPartnerSPN|故障转移伙伴 SPN|故障转移伙伴的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
  
## <a name="data-source-initialization-properties"></a>数据源初始化属性  
 `DBPROPSET_SQLSERVERDBINIT` 属性集中的以下属性允许应用程序指定 SPN。  
  
|“属性”|类型|用法|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR，读/写|指定服务器的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR，读/写|指定故障转移伙伴的 SPN。 默认值为空字符串，这会使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用访问接口生成的默认 SPN。|  
  
## <a name="data-source-properties"></a>数据源属性  
 `DBPROPSET_SQLSERVERDATASOURCEINFO` 属性集中的以下属性支持应用程序发现身份验证方法。  
  
|“属性”|类型|用法|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR，只读|返回用于连接的身份验证方法。 返回到应用程序的值是 Windows 返回到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的值。 以下列出的是可能的值：<br /><br /> -"NTLM"，使用 NTLM 身份验证打开连接时，将返回。<br />-"Kerberos"，使用 Kerberos 身份验证打开连接时，将返回。<br /><br /> 如果已经打开连接但无法确定身份验证方法，将返回 VT_EMPTY。<br /><br /> 只能在已经初始化数据源时读取此属性。 如果你尝试在初始化数据源之前读取的属性，IDBProperties::GetProperies 将返回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，根据需要，并将在 DBPROPSET_PROPERTIESINERROR 中设置 DBPROPSTATUS_NOTSUPPORTED此属性。 此行为符合 OLE DB 核心规范。|  
|SSPROP_MUTUALLYAUTHENICATED|VT_ BOOL，只读|如果建立连接的服务器之间已通过相互身份验证，则返回 VARIANT_TRUE；否则返回 VARIANT_FALSE。<br /><br /> 只能在已经初始化数据源时读取此属性。 如果尝试在初始化数据源之前读取的属性，IDBProperties::GetProperies 将返回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，根据需要，并将 DBPROPSET_ 中设置 DBPROPSTATUS_NOTSUPPORTED此属性的 PROPERTIESINERROR。 此行为是根据 OLE DB 核心规范<br /><br /> 如果针对未使用 Windows 身份验证的连接查询此属性，将返回 VARIANT_FALSE。|  
  
## <a name="ole-db-api-support-for-spns"></a>OLE DB API 对 SPN 的支持  
 下表对支持客户端连接中的 SPN 的 OLE DB 成员函数进行了说明：  
  
|成员函数|Description|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString*可以包含新关键字`ServerSPN`和`FailoverPartnerSPN`。|  
|IDataInitialize::GetInitializationString|如果 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 具有非默认值，则它们将包含通过在初始化字符串*ppwszInitString*关键字值的形式`ServerSPN`和`FailoverPartnerSPN`。 如果有默认值，这些关键字将不包括在初始化字符串中。|  
|IDBInitialize::Initialize|如果通过在数据源初始化属性中设置 DBPROP_INIT_PROMPT 启用了提示功能，将显示 OLE DB“登录”对话框。 这允许为主体服务器及其故障转移伙伴输入 SPN。<br /><br /> 提供程序字符串在 DPPROP_INIT_PROVIDERSTRING 中，如果设置，则将识别新关键字`ServerSPN`和`FailoverPartnerSPN`和使用它们的值，如果存在，来初始化 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN。<br /><br /> 可以调用 idbproperties:: Setproperties idbinitialize:: Initialize 调用之前设置属性 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN。 这是使用访问接口字符串的替代方法。<br /><br /> 如果在多个位置设置了某属性，以编程方式设置的值优先于在访问接口字符串中设置的值。 在初始化字符串中设置的值优先于在登录对话框中设置的值。<br /><br /> 如果同一关键字多次出现在访问接口字符串中，首次出现的值的优先级最高。|  
|IDBProperties::GetProperties|Idbproperties:: Getproperties 可以调用以获取值的新的数据源初始化属性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN，和的新数据源属性 SSPROP_AUTHENTICATIONMETHOD 和 SSPROP_MUTUALLYAUTHENTICATED。|  
|IDBProperties::GetPropertyInfo|Idbproperties:: Getpropertyinfo 将包括新的数据源初始化属性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 或新的数据源属性 SSPROP_AUTHENTICATION_METHOD 和 ssprop_mutuallyauthenticated 的值。|  
|IDBProperties::SetProperties|可以调用 idbproperties:: Setproperties 设置初始化属性 SSPROP_INITSERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 的新数据源的值。<br /><br /> 可以随时设置这些属性，不过如果数据源已经打开，将返回以下错误：DB_E_ERRORSOCCURRED，“多步 OLE DB 操作生成了错误。 检查每个 OLE DB 状态值（如果有）。 未执行任何操作。”|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (OLE DB)](sql-server-native-client-ole-db.md)  
  
  
