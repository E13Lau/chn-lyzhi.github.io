---
layout: post
title:  "iOS - AFNetWorking基础使用"
date:   2015-05-19 10:28
categories: jekyll update
tags: iOS
---

思路： 

- 有一个 BaseService 类，其他 Service 类继承该类。 
- 同样地，有一个 BaseModel 类，其他 Model 类继承该类 
- 在 BaseService 类中声明 AFHTTPRequestOperationManager 对象及 block 块

BaseService 类中 init 方法

```
- (instancetype)init
{
    self = [super init];
    if (self) {
        self.client = [[AFHTTPRequestOperationManager alloc] initWithBaseURL:[NSURL URLWithString:URL_BASE_SERVER]];
        self.client.requestSerializer = [AFJSONRequestSerializer serializer];
        self.client.responseSerializer = [AFJSONResponseSerializer serializer];
    }
    return self;
}
```
</br>
block 块声明于 BaseService.h 文件中

```
#import <Foundation/Foundation.h>
#import "AFNetworking.h"
#import "DataUtil.h"

typedef void(^CompletionHandler)(BOOL state,id object,NSError * error);
@interface BaseService : NSObject
S_PROPERTY(AFHTTPRequestOperationManager, client)
- (NSString *)getURLWithMainID:(int)mainID baseURL:(NSString *)baseURL;
@end
```
</br>
其中一个 Service 类中的方法：

```
#pragma -mark get guide list
- (void)getGuidesListWithCategoryId:(int)categoryId limit:(int)limit offset:(int)offset handler:(CompletionHandler)handler
{
    NSMutableDictionary *params = [[NSMutableDictionary alloc] init];
    NSString * url = [self getURLWithMainID:categoryId baseURL:URL_GUIDES_LIST];
    if (limit >= 0) {
        [params setObject:SNumberWithInt(limit) forKey:@"limit"];
    }
    if (offset >= 0) {
        [params setObject:SNumberWithInt(offset) forKey:@"offset"];
    }
    [self.client GET:url parameters:params success:^(AFHTTPRequestOperation *operation, id responseObject) {
        NSArray *array  = (NSArray *)responseObject;
        if (array) {
            NSMutableArray *result = [[NSMutableArray alloc] init];
            for (NSDictionary *object in array) {

                [result addObject:[self createGuideModel:object]];
            }
            handler(YES,result,nil);
        } else {
            handler(NO,nil,[NSError errorWithDomain:@"error" code:-1 userInfo:nil]);
        }
    } failure:^(AFHTTPRequestOperation *operation, NSError *error) {
        handler(NO, nil ,error);
    }];
}

#pragma mark -
- (GuideModel *)createGuideModel:(NSDictionary *)object
{
    if (!object) {
        return  nil;
    }
    GuideModel *guide = [[GuideModel alloc] init];
    guide.guideId = [object objectForKey:@"id"];
    guide.guideTitle = [object objectForKey:@"title"];
    guide.guideTime = [object objectForKey:@"time"];
    guide.guideName = [object objectForKey:@"name"];
    guide.guideCollectNums = [object objectForKey:@"collect_nums"];
    guide.guideCommentNums = [object objectForKey:@"comment_nums"];
    return guide;
}
```
</br>
在对应的声明该 model

```
@interface GuideModel : BaseModel

S_PROPERTY(NSString, guideId)

S_PROPERTY(NSString, guideTitle)

S_PROPERTY(NSString, guideName)

S_PROPERTY(NSString, guideImage)

S_PROPERTY(NSString, guideTime)

S_PROPERTY(NSString, guideCollectNums)

S_PROPERTY(NSString, guideLikeNums)

S_PROPERTY(NSString, guideCommentNums)
@end
```
其中 `#define S_PROPERTY(__TYPE,__NAME) @property (strong, nonatomic) __TYPE *__NAME;`

简单使用

```
- (void)loadDataWithFlag:(BOOL)flag {
    NSMutableArray *bottomArray = [NSMutableArray array];
    if (flag) {
        bottomArray = [NSMutableArray arrayWithArray:self.itemArray];
    }
    [self.service getActivityListWithLimit:15 offset:(int)bottomArray.count Handler:^(BOOL state, id object, NSError *error) {
        if (state) {
            [SVProgressHUD dismiss];
            [bottomArray addObjectsFromArray:object];
            self.itemArray = bottomArray;
            [self.tableView reloadData];
        } else {
            if (error) {
                NSString * errorString = [error.userInfo objectForKey:@"NSLocalizedDescription"];
                [SVProgressHUD showErrorWithStatus:errorString];
            }
        }
    }];
}
```

flag 标志为刷新加载更多而使用。 
self.itemArray 为 tableView 数据

