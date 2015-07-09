---
layout: post
title:  "iOS 开发-数组反向显示于 tableView。"
date:   2014-11-18 16:03
categories: jekyll update
tags: iOS
---


效果类似 iOS 上的系统秒表功能下的 tableView 显示方式。

代码如下

```
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    static NSString *Identifier = @"Cell";
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:Identifier];

    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:Identifier];
    }

    cell.textLabel.text = [self.timelist objectAtIndex:[self.timelist count]-indexPath.row-1];
    return cell;
}
```

其中
`cell.textLabel.text = [self.timelist objectAtIndex:[self.timelist count]-indexPath.row-1];`
为关键代码。
将对象下标设置为数组的数量减去位置下标减1