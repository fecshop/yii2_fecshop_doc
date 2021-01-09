关于平台账户权限
==========

> 品台账户描述


### 用户类型

`super admin`：平台总账户，超级账户admin，可以看所有的信息，也就是账号 `admin`

`common admin`：普通admin账户

### 数据库表customer

1.表加上类型字段

1.1表字段`type`: 1代表`super admin`，2代表普通admin账户`common admin`

1.2表字段`parent_id`，此字段只针对`common user`有效，也就是该用户只能
看到`own_id = parent_id`的数据（最多看到的数据）

### 账户登录

1.1根据登录的账户，获取到账户的type，将该信息保存到jwt-token里面，登录后，通过token解码，
获取当前用户的type

1.2获取相应的菜单权限，也就是能看到的菜单，渲染前端vue

### 请求数据

1.vue点击菜单访问页面，进行后端数据请求

2.go部分，先判断是否有url请求权限，如果没有权限，直接返回权限拒绝信息

3.如果用户有url请求权限，则进行数据请求，然后查看用户的数据获取权限

3.1如果用户是`super admin`，则没有限制

3.2如果用户是`common admin`，则需要在数据获取部分的where部分加上 own_id = customer_id 

4返回数据。

### 实现

1.数据库表添加字段，增删改查修改

2.后端gin对每一个url做好权限控制，那些url允许上面的那些角色访问，需要角色访问受限的，就加上。
譬如，只允许超级账户访问就加上`handle.PermissionSuperAdmin`
, 通用的权限限制就用`handle.PermissionAdmin`




























