# RDS for PostgreSQL用户权限设置 {#concept_266125 .concept}

RDS for PostgreSQL没有开放超级用户，这给很多上云的用户带来困难，RDS for PostgreSQL这样做有如下原因：

-   PostgreSQL的superuser拥有几乎全部的数据库权限，甚至可以直接修改系统表，潜在风险相当大。
-   RDS for PostgreSQL使用superuser运维实例，例如管理流复制、备份等这些操作，用户是不需要关心的，换句话说它应该完全的交给云服务来处理。
-   RDS for PostgreSQL的普通用户权限是能够满足应用需求的，用户可以管理自己在云上的数据。

## 基本原则 {#section_lfl_zom_u4u .section}

-   一个普通用户只能在自己作为owner（所有者）的数据库下创建schema。
-   数据库下的对象有一个所属的schema，普通用户可以在public下创建对象（如table），在其他schema下创建对象需要是schema的owner或有特别的授权。
-   管理一个数据库对象，需要是对象的owner（在用户组权限之外）。

## 常见问题及解决方法 {#section_dzx_9ux_kip .section}

在多用户环境下，RDS for PostgreSQL用户容易遇到无法使用普通用户管理其他普通用户创建的对象，出现操作对象无权限的问题。

通常可以用控制台创建的高权限账号创建管理员账号，然后将子账号的权限授予管理员账号。使用这样的用户组可以做到使用一个管理员账号管理所在组内的所有其他普通用户以及他们的对象，既可以管理多个用户的对象，又可以实现一定程度上的权限隔离，同时权限又不会过大，推荐在云上使用该方式管理自己的实例。

**说明：** 管理员账号默认具有 INHERIT权限，INHERIT权限决定一个角色是否继承它所在组的角色的权限。 一个带有INHERIT属性的角色可以自动使用已经赋与它直接或间接所在组的任何权限。

