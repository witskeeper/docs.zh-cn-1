---
title: ICorProfilerInfo2::GetArrayObjectInfo 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetArrayObjectInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetArrayObjectInfo
helpviewer_keywords:
- ICorProfilerInfo2::GetArrayObjectInfo method [.NET Framework profiling]
- GetArrayObjectInfo method [.NET Framework profiling]
ms.assetid: bda75017-739f-4ce5-9000-f3b526e8473c
topic_type:
- apiref
ms.openlocfilehash: 97b127c9a6aac0a0fefe25faf294791dcd2c8e41
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2019
ms.locfileid: "74436031"
---
# <a name="icorprofilerinfo2getarrayobjectinfo-method"></a>ICorProfilerInfo2::GetArrayObjectInfo 方法
获取有关数组对象的详细信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetArrayObjectInfo(  
    [in] ObjectID objectId,  
    [in] ULONG32 cDimensions,  
    [out, size_is(cDimensions), length_is(cDimensions)] ULONG32 pDimensionSizes[],  
    [out, size_is(cDimensions), length_is(cDimensions)] int pDimensionLowerBounds[],  
    [out] BYTE **ppData);  
```  
  
## <a name="parameters"></a>参数  
 `objectId`  
 中有效数组对象的 ID。  
  
 `cDimensions`  
 中数组的秩（维数）。  
  
 `pDimensionSizes`  
 弄一个包含整数的数组，每个整数表示数组维度的大小。  
  
 `pDimensionLowerBounds`  
 弄一个包含整数的数组，其中每个整数表示数组维度的下限。  
  
 `ppData`  
 弄一个指针，它指向数组的原始缓冲区的地址，该地址根据C++约定进行布局。  
  
## <a name="remarks"></a>备注  
 `pDimensionSizes` 和 `pDimensionLowerBounds` 是并行数组，因此位于每个数组中同一索引处的元素是同一实体的特征。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **头文件：** CorProf.idl、CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [ICorProfilerInfo 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
