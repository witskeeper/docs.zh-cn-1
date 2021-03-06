---
title: ISymUnmanagedMethod::GetSequencePoints 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetSequencePoints
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetSequencePoints
helpviewer_keywords:
- ISymUnmanagedMethod::GetSequencePoints method [.NET Framework debugging]
- GetSequencePoints method [.NET Framework debugging]
ms.assetid: f909ac48-3d8f-49fb-a369-e3d9959151cd
topic_type:
- apiref
ms.openlocfilehash: 75d477af7395a9b7d3328b2a5787f810733f3749
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448872"
---
# <a name="isymunmanagedmethodgetsequencepoints-method"></a>ISymUnmanagedMethod::GetSequencePoints 方法
获取此方法中的所有序列点。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetSequencePoints(  
    [in]  ULONG32  cPoints,  
    [out] ULONG32  *pcPoints,  
    [in, size_is(cPoints)] ULONG32  offsets[],  
    [in, size_is(cPoints)] ISymUnmanagedDocument* documents[],  
    [in, size_is(cPoints)] ULONG32  lines[],  
    [in, size_is(cPoints)] ULONG32  columns[],  
    [in, size_is(cPoints)] ULONG32  endLines[],  
    [in, size_is(cPoints)] ULONG32  endColumns[]);  
```  
  
## <a name="parameters"></a>参数  
 `cPoints`  
 中接收 `offsets`、`documents`、`lines`、`columns`、`endLines`和 `endColumns` 数组大小的 `ULONG32`。  
  
 `pcPoints`  
 弄指向 `ULONG32` 的指针，该指针接收包含序列点所需的缓冲区的长度。  
  
 `offsets`  
 中一个数组，在其中存储序列点从方法的开头开始的 Microsoft 中间语言（MSIL）偏移量。  
  
 `documents`  
 中要在其中存储序列点所在的文档的数组。  
  
 `lines`  
 中要在其中存储序列点所在的文档中的行的数组。  
  
 `columns`  
 中要在其中存储序列点所在的文档中的列的数组。  
  
 `endLines`  
 中序列点结束的文档中的行的数组。  
  
 `endColumns`  
 中序列点结束的文档中的列的数组。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功，则 S_OK;否则，E_FAIL 或其他一些错误代码。  
  
## <a name="requirements"></a>要求  
 **标头：** CorSym，CorSym  
  
## <a name="see-also"></a>另请参阅

- [ISymUnmanagedMethod 接口](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedmethod-interface.md)
