---
title: CorElementType 枚举
ms.date: 03/30/2017
api_name:
- CorElementType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorElementType
helpviewer_keywords:
- CorElementType enumeration [.NET Framework metadata]
ms.assetid: c3809c8f-1737-4f0f-9442-0c01ee689871
topic_type:
- apiref
ms.openlocfilehash: 0ce84e1545523302cd47e60b9f047bc470e6bf0f
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2019
ms.locfileid: "74443625"
---
# <a name="corelementtype-enumeration"></a>CorElementType 枚举

指定公共语言运行时 <xref:System.Type>、类型修饰符或元数据类型签名中的类型的相关信息。

## <a name="syntax"></a>语法

```cpp
typedef enum CorElementType {
    ELEMENT_TYPE_END            = 0x0,
    ELEMENT_TYPE_VOID           = 0x1,
    ELEMENT_TYPE_BOOLEAN        = 0x2,
    ELEMENT_TYPE_CHAR           = 0x3,
    ELEMENT_TYPE_I1             = 0x4,
    ELEMENT_TYPE_U1             = 0x5,
    ELEMENT_TYPE_I2             = 0x6,
    ELEMENT_TYPE_U2             = 0x7,
    ELEMENT_TYPE_I4             = 0x8,
    ELEMENT_TYPE_U4             = 0x9,
    ELEMENT_TYPE_I8             = 0xa,
    ELEMENT_TYPE_U8             = 0xb,
    ELEMENT_TYPE_R4             = 0xc,
    ELEMENT_TYPE_R8             = 0xd,
    ELEMENT_TYPE_STRING         = 0xe,

    ELEMENT_TYPE_PTR            = 0xf,
    ELEMENT_TYPE_BYREF          = 0x10,

    ELEMENT_TYPE_VALUETYPE      = 0x11,
    ELEMENT_TYPE_CLASS          = 0x12,
    ELEMENT_TYPE_VAR            = 0x13,
    ELEMENT_TYPE_ARRAY          = 0x14,
    ELEMENT_TYPE_GENERICINST    = 0x15,
    ELEMENT_TYPE_TYPEDBYREF     = 0x16,

    ELEMENT_TYPE_I              = 0x18,
    ELEMENT_TYPE_U              = 0x19,
    ELEMENT_TYPE_FNPTR          = 0x1B,
    ELEMENT_TYPE_OBJECT         = 0x1C,
    ELEMENT_TYPE_SZARRAY        = 0x1D,
    ELEMENT_TYPE_MVAR           = 0x1e,

    ELEMENT_TYPE_CMOD_REQD      = 0x1F,
    ELEMENT_TYPE_CMOD_OPT       = 0x20,

    ELEMENT_TYPE_INTERNAL       = 0x21,
    ELEMENT_TYPE_MAX            = 0x22,

    ELEMENT_TYPE_MODIFIER       = 0x40,
    ELEMENT_TYPE_SENTINEL       = 0x01 | ELEMENT_TYPE_MODIFIER,
    ELEMENT_TYPE_PINNED         = 0x05 | ELEMENT_TYPE_MODIFIER

} CorElementType;
```

## <a name="members"></a>Members

|成员|说明|
|------------|-----------------|
|`ELEMENT_TYPE_END`|内部使用。|
|`ELEMENT_TYPE_VOID`|Void 类型。|
|`ELEMENT_TYPE_BOOLEAN`|布尔类型|
|`ELEMENT_TYPE_CHAR`|一个字符类型。|
|`ELEMENT_TYPE_I1`|有符号1字节整数。|
|`ELEMENT_TYPE_U1`|1 字节无符号整数。|
|`ELEMENT_TYPE_I2`|有符号的2字节整数。|
|`ELEMENT_TYPE_U2`|无符号2字节整数。|
|`ELEMENT_TYPE_I4`|有符号4字节整数。|
|`ELEMENT_TYPE_U4`|4字节无符号整数。|
|`ELEMENT_TYPE_I8`|8字节有符号整数。|
|`ELEMENT_TYPE_U8`|8字节无符号整数。|
|`ELEMENT_TYPE_R4`|4字节浮点数。|
|`ELEMENT_TYPE_R8`|8字节浮点数。|
|`ELEMENT_TYPE_STRING`|System.string 类型。|
|`ELEMENT_TYPE_PTR`|指针类型修饰符。|
|`ELEMENT_TYPE_BYREF`|引用类型修饰符。|
|`ELEMENT_TYPE_VALUETYPE`|值类型修饰符。|
|`ELEMENT_TYPE_CLASS`|类类型修饰符。|
|`ELEMENT_TYPE_VAR`|类变量类型修饰符。|
|`ELEMENT_TYPE_ARRAY`|多维数组类型修饰符。|
|`ELEMENT_TYPE_GENERICINST`|泛型类型的类型修饰符。|
|`ELEMENT_TYPE_TYPEDBYREF`|类型化的引用。|
|`ELEMENT_TYPE_I`|本机整数的大小。|
|`ELEMENT_TYPE_U`|无符号本机整数的大小。|
|`ELEMENT_TYPE_FNPTR`|指向函数的指针。|
|`ELEMENT_TYPE_OBJECT`|System.object 类型。|
|`ELEMENT_TYPE_SZARRAY`|一维的、从零开始的下限数组类型修饰符。|
|`ELEMENT_TYPE_MVAR`|方法变量类型修饰符。|
|`ELEMENT_TYPE_CMOD_REQD`|C 语言必需的修饰符。|
|`ELEMENT_TYPE_CMOD_OPT`|C 语言可选修饰符。|
|`ELEMENT_TYPE_INTERNAL`|内部使用。|
|`ELEMENT_TYPE_MAX`|无效类型。|
|`ELEMENT_TYPE_MODIFIER`|内部使用。|
|`ELEMENT_TYPE_SENTINEL`|作为参数数目可变的列表的 sentinel 的类型修饰符。|
|`ELEMENT_TYPE_PINNED`|内部使用。|

## <a name="remarks"></a>备注

类型修饰符构成了用于表示更复杂类型的基础。 `CorElementType` 类型修饰符值应用于在类型签名中紧跟在其后面的值。 按照下表中的说明，`CorElementType` 类型修饰符值之后的值可以是一个 `CorElementType` 简单类型值、一个元数据标记或其他值。

> [!NOTE]
> 所有数字（*数字*、*参数计数*、*元数据标记*、*排名*、*计数*和*界限*）都存储为压缩整数。 有关详细信息，请参阅 ECMA 网站上的[标准 ECMA-335-公共语言基础结构（CLI）](https://go.microsoft.com/fwlink/?LinkID=116487) 。

|类型修饰符|格式|
|-------------------|------------|
|`ELEMENT_TYPE_PTR`|ELEMENT_TYPE_PTR \<`CorElementType` 值 >|
|`ELEMENT_TYPE_BYREF`|ELEMENT_TYPE_BYREF \<`CorElementType` 值 >|
|`ELEMENT_TYPE_VALUETYPE`|`mdTypeDef` 元数据标记 \<ELEMENT_TYPE_VALUETYPE >|
|`ELEMENT_TYPE_CLASS`|`mdTypeDef` 元数据标记 \<ELEMENT_TYPE_CLASS >|
|`ELEMENT_TYPE_VAR`|\<号码 ELEMENT_TYPE_VAR >|
|`ELEMENT_TYPE_ARRAY`|ELEMENT_TYPE_ARRAY \<`CorElementType` 值 > \<> \<> \<> \<> \<>|
|`ELEMENT_TYPE_GENERICINST`|ELEMENT_TYPE_GENERICINST \<`mdTypeDef` 元数据令牌 > \<参数计数 > \<arg1 > ... \<argN >|
|`ELEMENT_TYPE_FNPTR`|ELEMENT_TYPE_FNPTR \<函数的完整签名，包括调用约定 >|
|`ELEMENT_TYPE_SZARRAY`|ELEMENT_TYPE_SZARRAY \<`CorElementType` 值 >|
|`ELEMENT_TYPE_MVAR`|\<号码 ELEMENT_TYPE_MVAR >|
|`ELEMENT_TYPE_CMOD_REQD`|ELEMENT_TYPE_\<`mdTypeRef` 或 `mdTypeDef` 的元数据标记 >|
|`ELEMENT_TYPE_CMOD_OPT`|E_T_CMOD_OPT \<`mdTypeRef` 或 `mdTypeDef` 的元数据标记 >|

## <a name="requirements"></a>要求

**平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** Corhdr。h

**.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>另请参阅

- [Metadata 枚举](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
