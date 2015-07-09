---
layout: post
title:  "iOS 开发－实现TableView的编辑功能以删除数据"
date:   2014-04-27 00:05
categories: jekyll update
tags: iOS
---


关键代码如下：

```
- (void)viewDidLoad
{    
self.editButtonItem.title = @"编辑";
self.navigationItem.leftBarButtonItem = self.editButtonItem;
}
//修改删除按钮的文字
-(NSString *)tableView:(UITableView *)tableView titleForDeleteConfirmationButtonForRowAtIndexPath:(NSIndexPath *)indexPath {
    return @"删除";
}
//设置Edit文本
- (void)setEditing:(BOOL)editing animated:(BOOL)animated
{
    [super setEditing:editing animated:animated];
    if (self.editing) {
        self.editButtonItem.title = @"完成";
    } else {
        self.editButtonItem.title = @"编辑";
    }
}
- (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle
forRowAtIndexPath:(NSIndexPath *)indexPath
{
    if (editingStyle == UITableViewCellEditingStyleDelete)
    {
        [self.toDoItems removeObjectAtIndex: indexPath.row];
        //        [tableView insertRowsAtIndexPaths:[NSArray arrayWithObject:indexPath]
        //                         withRowAnimation:UITableViewRowAnimationFade];
        [self.tableView deleteRowsAtIndexPaths:[NSMutableArray arrayWithObject:indexPath]
                         withRowAnimation:UITableViewRowAnimationFade];
        [self.tableView reloadData];
    }
}
//开启向左滑动显示删除功能
- (BOOL)tableView:(UITableView *)tableView canMoveRowAtIndexPath:(NSIndexPath *)indexPath
{
    // Return NO if you do not want the item to be re-orderable.
    return YES;
}
```