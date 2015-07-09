---
layout: post
title:  "iOS - 使用QBImagePickerController选取图片"
date:   2015-05-09 10:48
categories: jekyll update
tags: iOS
---

使用QBImagePickerController选取图片

首先使用pod引入

```
pod 'QBImagePickerController', '~>2.5.1'  
#- Homepage: https://github.com/questbeat/QBImagePicker  
#3.0需要iOS SDK 8.0
```

导入 `#import <QBImagePickerController.h>`

声明并设置delegate
`QBImagePickerController * imagePickerController;`

init

```
- (void)initQBimagePickerController {
    imagePickerController = [[QBImagePickerController alloc]init];
    imagePickerController.prompt = @"选择图片";
    imagePickerController.allowsMultipleSelection = YES;
    imagePickerController.showsNumberOfSelectedAssets = YES;
    imagePickerController.delegate = self;
}
```

delegate方法

```
#pragma mark imagePickerControllerdelegate
-(void)qb_imagePickerController:(QBImagePickerController *)imagePickerController didSelectAssets:(NSArray *)assets {
    [self dismissViewControllerAnimated:YES completion:^{
        NSLog(@"%@",assets);
        [imageMutableArray removeAllObjects];
        for (ALAsset * asset in assets) {
            
            ALAssetRepresentation *assetRep = [asset defaultRepresentation];
            CGImageRef imgRef = [assetRep fullResolutionImage];   //获取高清图片
            UIImage *img = [UIImage imageWithCGImage:imgRef
                                               scale:assetRep.scale
                                         orientation:(UIImageOrientation)assetRep.orientation];
            CGImageRef ref = [asset thumbnail];    //获取缩略图
            UIImage *thumbnailImg = [[UIImage alloc]initWithCGImage:ref];
            [imageMutableArray addObject:thumbnailImg];
        }
        [imageMutableArray addObject:[UIImage imageNamed:@"更多"]];
        [self.imageCollectionView reloadData];
    }];
}

-(void)qb_imagePickerControllerDidCancel:(QBImagePickerController *)imagePickerController {
    [self dismissViewControllerAnimated:YES completion:^{
        
    }];
}
```

附：

获得的ALAsset对象就是相片对象：其中有相片的缩略图，全屏图，高清图，url等属性。
`ALAsset *result = [assets objectAtIndex:index];`

获取url：
String类型：
`NSString *url = [[[result
defaultRepresentation]url]description];`

URL类型：
`NSURL *url = [[result defaultRepresentation]url];`

获取缩略图：
`CGImageRef  ref = [result thumbnail];`
`UIImage *img = [[UIImage alloc]initWithCGImage:ref];`

获取全屏相片：
`CGImageRef ref = [[result  defaultRepresentation]fullScreenImage];`
`UIImage *img = [[UIImage alloc]initWithCGImage:ref];`

获取高清相片：
`CGImageRef ref = [[result  defaultRepresentation]fullResolutionImage];`
`UIImage *img = [[UIImage alloc]initWithCGImage:ref];`


存在问题：

* 该PickerController会保存每次的选择项，暂没找到方法去掉
* self.imageCollectionView显示图片的CollectionView又一个恒定的显示在最后一项的加号，如何更好的实现