---
layout: post
title:  "iOS 开发-CollectionView Test 记录"
date:   2014-12-24 17:57
categories: jekyll update
tags: iOS
---

首先storyboard拖拽进一个CollectionView，连接到.m，创建属性。

当前viewController继承
`<UICollectionViewDataSource,UICollectionViewDelegate,UICollectionViewDelegateFlowLayout>`

viewDidLoad方法中加上

```
self.collectionView.delegate = self;  
self.collectionView.dataSource = self;
```

添加代理方法

```
-(NSInteger)numberOfSectionsInCollectionView:(UICollectionView *)collectionView {
    return 1;
}

-(NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section {
    return [menuData count];
}

-(UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath {
//    UICollectionViewCell * cell = (UICollectionViewCell *)[collectionView dequeueReusableCellWithReuseIdentifier:@"CollectionCell" forIndexPath:indexPath];
    
    XYZGGCollectionViewCell * cell = [collectionView dequeueReusableCellWithReuseIdentifier:@"cell" forIndexPath:indexPath];

    cell.cellLabel.text = menuData[indexPath.row];
    return cell;
}
```

其中cell使用新类控制。
创建`CollectionViewCell`类，继承自`UICollectionViewCell`，带xib。

xib中设置cell视图。
在自定义`CollectionViewCell`类中添加方法

```
-(instancetype)initWithFrame:(CGRect)frame {
    self = [super initWithFrame:frame];
    if (self)
    {
        // 初始化时加载collectionCell.xib文件
        NSArray *arrayOfViews = [[NSBundle mainBundle] loadNibNamed:@"XYZGGCollectionViewCell" owner:self options:nil];
        
        // 如果路径不存在，return nil
        if (arrayOfViews.count < 1)
        {
            return nil;
        }
        // 如果xib中view不属于UICollectionViewCell类，return nil
        if (![[arrayOfViews objectAtIndex:0] isKindOfClass:[UICollectionViewCell class]])
        {
            return nil;
        }
        // 加载nib
        self = [arrayOfViews objectAtIndex:0];
    }
    return self;
}
```

在使用collectionViewcontroller中的viewDidLoad中添加

```
[self.collectionView registerClass:[XYZGGCollectionViewCell class] forCellWithReuseIdentifier:@"cell"];
```