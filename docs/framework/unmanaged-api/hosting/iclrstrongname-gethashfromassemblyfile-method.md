---
title: ICLRStrongName::GetHashFromAssemblyFile 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.GetHashFromAssemblyFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::GetHashFromAssemblyFile
helpviewer_keywords:
- ICLRStrongName::GetHashFromAssemblyFile method [.NET Framework hosting]
- GetHashFromAssemblyFile method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 0b67ea03-d474-4605-acaa-57455790250c
topic_type:
- apiref
ms.openlocfilehash: 3fd9efd3961be1d6e6e91b881327628c598e364e
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73092727"
---
# <a name="iclrstrongnamegethashfromassemblyfile-method"></a>ICLRStrongName::GetHashFromAssemblyFile 方法
使用指定的哈希算法获取指定程序集文件的哈希。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetHashFromAssemblyFile (  
    [in]  LPCSTR   szFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE     *pbHash,  
    [in]  DWORD    cchHash,  
    [out] DWORD    *pchHash  
);  
```  
  
## <a name="parameters"></a>参数  
 `szFilePath`  
 中要进行哈希处理的文件的路径。  
  
 `piHashAlg`  
 [in，out]指定哈希算法的常量。 使用零作为默认哈希算法。  
  
 `pbHash`  
 弄返回的哈希缓冲区。  
  
 `cchHash`  
 中请求的最大 `pbHash`大小。  
  
 `pchHash`  
 弄返回 `pbHash`的大小（以字节为单位）。  
  
## <a name="return-value"></a>返回值  
 如果方法已成功完成，则 `S_OK`;否则，表示失败的 HRESULT 值（请参阅列表的[常见 HRESULT 值](https://go.microsoft.com/fwlink/?LinkId=213878)）。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MetaHost  
  
 **库：** 作为资源包括在 Mscoree.dll 中  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [GetHashFromAssemblyFileW 方法](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-gethashfromassemblyfilew-method.md)
- [ICLRStrongName 接口](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
