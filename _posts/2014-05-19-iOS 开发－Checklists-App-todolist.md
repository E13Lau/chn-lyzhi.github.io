---
layout: post
title:  "iOS 开发－Checklists-App-todolist"
date:   2014-05-19 20:00
categories: jekyll update
tags: iOS
---


* SUMMARY:该界⾯面需要被重新命名为Edit Item
* SUMMARY:简单美化
* SUMMARY:当触碰”+“添加按钮的时候往列表中添加⼀一个伪项⺫⽬目
* SUMMARY:当⽤用户更改代办事项时(如添加⼀一个新项⺫⽬目,开启/关闭勾选标志等),将待办事项保存到⽂文件 中。
* SUMMARY:创建⼀一个新的界⾯面,可以让⽤用户添加/编辑代办事务清单
* SUMMARY:添加⼀一个⽂文本输⼊入框,让⽤用户可以使⽤用内置键盘来输⼊入信息
* SUMMARY:在主界⾯面的表视图中添加新创建的ChecklistItem对象
* SUMMARY:将所有的代办事务清单保存在⽂文件中,然后在需要的时候从该⽂文件中加载。
* SUMMARY:当触碰代办事务清单列表中的某⼀一项时,会显⽰示该清单所属的所有代办事项
* SUMMARY:当应⽤用重新启动时从该⽂文件加载代办事项清单。
* SUMMARY:添加⼀一个navigation controller
* SUMMARY:借⽤用storyboarding的⼒力量来创建⼀一个Add Item界⾯面
* SUMMARY:当⽤用户触碰back按钮返回主界⾯面的时候,我们需要从NSUserDefaults设置中删除刚才所保存的数 值。通常情况下,
*  当我们将某个数值设置为,就意味着“没有数值”。为神⻢马是-1?因为我们在计 算⾏行编号的时候是从0开始的,因此总是会使⽤用0或者任何⼀一个整
*  数。-1不是⼀一个有效的⾏行编号,⽽而 因为它是⼀一个负值,所以就很容易在debug的过程中观察到可能出现的情况。
* SUMMARY:根据某个特定的顺序对其中的项⺫⽬目进⾏行排序。这⾥里我 们将根据事项名称对列表进⾏行排序。
* SUMMARY:我们需要给它提供⼀一个已有的checklistItem对象
* SUMMARY:我们需要在⽂文本域中显⽰示现有项⺫目的⽂文本内容
* SUMMARY:给checklist添加图标
* SUMMARY:在导航栏上⾯面放⼀一个“+”添加按钮
* SUMMARY:使⽤用⽂文本输⼊入框⾥里⾯面所输入的⽂文本来创建⼀一个新的ChecklistItem
* SUMMARY:添加启动界面
* SUMMARY:判断何时⽤用户触碰Add Item界⾯面上的Cancel或Done按钮
* SUMMARY:当⽤用户触碰done的时候,更新现有项⺫⽬目的内容,⽽而不是添加⼀一个新的项⺫⽬目。
* SUMMARY:为了让代办事务清单中的事项可以持久保存,判断该把保存这些信息的⽂文件放到⽂文件系统的何 处。
* SUMMARY:在从主界⾯面(AllListsViewController)到checklist界⾯面(ChecklistViewControl
*  ler)的segue上,我们 需要编写代码将选中的checklist的⾏行编号保存到NSUserDefaults中。这样我们就可以让应⽤用记住用户所选择的checklist了。当然,或许你觉得保存checklist的名称⽐比⾏行编号更⼈人性化。不过想想⼀一种 可能,如果两个checklists的名称相同肿么办?虽然这种情况⽐比较罕⻅见,不过⽤用户不是完全例理性 的,总有这种可能会出现。因此使⽤用⾏行编号就可以确保应⽤用总是会选择正确的checlist
* SUMMARY:当应⽤用启动时如果NSUserDefaults中保存的数值不是-1,那么我们就知道⽤用户之前在查看checklist 中的内容 ,此时就可以⼿手动执⾏行segue切换到对应⾏行的ChecklistViewController>
* SUMMARY:可以在主界⾯面上显⽰示每个checklist⾥里⾯面还有多少代办事项没有完成。
* SUMMARY:创建⼀一个新的界⾯面,⽤用于显⽰示所有的代办事务清单
* SUMMARY:用到NSUserDefaults来记录相关信息,判断⽤用户是否是⾸首次打 开应⽤用。如果是,就创建⼀一个新的Checklist对象
* SUMMARY:允许⽤用户触碰某⼀一⾏行来打开或关闭选中标志。
* SUMMARY:使⽤用swipe-to-delete(滑动删除)的⽅方式来删除已有项⺫⽬目
* SUMMARY:在应⽤用的界⾯面上放置⼀一个表视图
* SUMMARY:打开Add Item界⾯面让⽤用户输⼊入项⺫⽬目的⽂文字描述。
* SUMMARY:在表视图⾥里⾯面填充数据

***循序为倒序***