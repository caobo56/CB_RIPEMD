# CB_RIPEMD
RIPEMD算法，目前只有RIPEMD-160。

是从CoreBitcoin 项目摘出来的，目的是方便查找RIPEMD-160。

我之前的CBBase58也有这部分代码，但单独放出来方便查找。

RIPEMD-160的算法是在 NSData+Hashing.h 中

NSData+Hashing.h  在项目的CB_RIPEMD/RIPEMD/路径下

下面是 NSData+Hashing.h 的接口层
```
//
//  NSData+Hashing.h
//  BitcoinSwift
//
//  Created by Kevin Greene on 6/19/14.
//  Copyright (c) 2014 DoubleSha. All rights reserved.
//

#import <Foundation/Foundation.h>

@interface NSData (Hashing)

/// Returns the SHA-256 hash of self.
- (NSData *)SHA256Hash;

/// Returns the RIPEMD-160 hash of self.
- (NSData *)RIPEMD160Hash;

/// Performs the HMAC512-SHA256 algorithm on self using key and stores the result in digest.
- (void)HMACSHA512WithKey:(NSData *)key digest:(NSMutableData *)digest;

@end
```

目前该 repo 只有 RIPEMD-160

计划是将 RIPEMD 下的相关算法都集成一下，包括（128、160、256和320），回头慢慢补充更新。

# RIPEMD算法
RIPEMD（RACE Integrity Primitives Evaluation Message Digest，RACE原始完整性校验消息摘要），是Hans Dobbertin等3人在md4,md5的基础上，于1996年提出来的。算法共有4个标准128、160、256和320，其对应输出长度分别为16字节、20字节、32字节和40字节。不过，让人难以致信的是RIPEMD的设计者们根本就没有真正设计256和320位这2种标准，他们只是在128位和160位的基础上，修改了初始参数和s-box来达到输出为256和320位的目的。所以，256位的强度和128相当，而320位的强度和160位相当。RIPEMD建立在md的基础之上，所以，其添加数据的方式和md5完全一样。
