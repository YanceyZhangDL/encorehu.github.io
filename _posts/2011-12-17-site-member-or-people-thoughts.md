---
layout: post
permalink: /site-member-or-people-thoughts
title: Django:DDTCMS关于网站用户和真人的想法
---

# Django:DDTCMS关于网站用户和真人的想法 #


    Django:DDTCMS关于网站用户和真人的想法



    写于2009-3-23,一直没有共享出来.

    网络用户和真是用户有什么区别和联系？

    一、网站上的用户是真实用户在使用。

    必须有一个人坐在电脑前，使用其帐户（网络用户）进行操作，

    虚拟用户被真实用户操作（机器制作的程序代替虚拟用户除外）

    二、一个ID是独一无二的，用户名唯一，你用了别人就不能用

    一个真人的名字是可以重复的，一个真人可以有多个ID（多个网站，一个网站多个ID）

    一个ID对应的必须是一个个人，仅有一个，多个ID可能均只对应相同的一个人。

    真人为本，网络用户是壳，是马甲，是角色，从属于真人。

    建立用户，用户名和密码，入库

    对于网站来说，个人用户帐户是真实的，现实真人是虚拟的。网站以人为本，应该是以用户为本，以用户帐号后面的真人为本。

    网站用户：

    用户名

    密码

    虚拟性别（可以让真人感觉一些充当异性的感觉）

    虚拟头像（让自己有个别的样子）

    帐户创建日期（网站虚拟生日）

    短信息

    真人：

    公共信息（大家都在用）：姓名，性别，照片

    私人信息（隐私）：生日（年龄），地址（邮箱，家庭住址，办公等），身高，体重，个人习惯

    网站管理这些，应该用两套系统，用宽松的联系组合在一起，可以考虑实名认证，和手机绑定的办法确定真人。

    网站的时间记录以用户为主，用户最好不能删除，因为很多用户在网站生产了信息（无论它是有用信息还是垃圾信息），其他记录关联到用户了。如果删除用户的话，关联被破坏，信息就不完整。

    如果数据库的设计式级联删除数据的话，用户被删除，就会相应删除很多其他模块的记录，得不偿失。

    那么如何进行网站用户的销户处理

    采取什么办法？

    设置用户状态，销户后将用户的有效状态设置为无效，但记录仍然保存。

    django中用户名是唯一的，这样，一个用户销户（设置状态为无效）后，同一个用户名不能再次被注册。销户后，可以采取在用户名后加一个后缀，类似于"__DEL20090320153204ETE"，这样DELETE被拆开中间的20090320153204是删除（设置为无效）时间戳。如果要恢复这个用户的话，就把这个后缀删除。这样要求用户名称中不要有2个连续的下划线“__”和“DEL”相连。这样用户名至少有16+用户名长度的位数。

    以后在用户销户后，其他模块中的相关记录（关联的并不是用户名，而是用户的ID）就可以判断用户后缀了。

    对于真人来说，其信息的管理，采取设置真人信息从属于网站用户的办法，django中就是

    zhenren=models.foriegnKey（User）的办法，但是数据库中可以为空，填写表单的时候也可以为空。因为真人并不是每个人都在你的网站上网并成为你的用户。比如说刘德华，张学友之类，不可能是你网站的用户吧。但是人物栏目并不一定要求他们到网站注册成用户。但是一旦他们到网站来注册了，我们就可以帮他把其个人资料关联到他在网站注册好的用户。