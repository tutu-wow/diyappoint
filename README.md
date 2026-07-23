# diyappoint
DIY手工社预约管理系统
本文注重于计算机毕业设计选题指导，列出题目均有源码， 大家可以去【公众号】(毕业终点站)获取或者加我【qq】(2112698948)提意见(别忘记Star哟)。备注：git

声明：仅用于学习使用，请勿用于任何商业行为！

1.系统非商用，非开源，非无偿。

2.由本人开发，如需源码，请联系以下方式，qq:2112698948。

3.项目有很多，并未全部上传，如果未找到想要的，可直接咨询。

<font style="color:#117CEE;">🎈</font><font style="color:#117CEE;">系统亮点</font>:<font style="color:#2F8EF4;">Echarts图形化分析、腾讯地图API；</font>

# <font style="color:rgb(72, 179, 120);">一.系统开发工具与环境搭建</font>
## <font style="color:rgb(38, 38, 38);">1.系统设计开发工具</font>
<font style="color:rgb(38, 38, 38);">  
</font><font style="color:rgb(38, 38, 38);">后端使用Java编程语言的Spring boot框架  
</font><font style="color:rgb(38, 38, 38);">项目架构：B/S架构  
</font><font style="color:rgb(38, 38, 38);">运行环境：win10/win11、jdk17</font>

<font style="color:rgb(38, 38, 38);">  
</font><font style="color:rgb(72, 179, 120);">前端：</font><font style="color:rgb(38, 38, 38);">  
</font><font style="color:rgb(38, 38, 38);">技术：框架Vue.js；UI库：ElementUI；   
</font><font style="color:rgb(38, 38, 38);">开发工具：Visual Studio Code；</font>

---

<font style="color:rgb(38, 38, 38);">  
</font><font style="color:rgb(72, 179, 120);">后端:</font><font style="color:rgb(38, 38, 38);">  
</font><font style="color:rgb(38, 38, 38);">技术：Java语言、mybatis plus、Spring boot框架；   
</font><font style="color:rgb(38, 38, 38);">开发工具：IDEA 2023.3.3版本；</font>

---

<font style="color:rgb(38, 38, 38);">  
</font><font style="color:rgb(72, 179, 120);">数据库：</font><font style="color:rgb(38, 38, 38);">  
</font><font style="color:rgb(38, 38, 38);">数据库：mysql5.7/8.0   
</font><font style="color:rgb(38, 38, 38);">数据库工具：Navicat12版本；</font>

---

# <font style="color:rgba(72,179,120,1);">二.系统功能需求分析</font>
<font style="color:rgba(72,179,120,1);">（</font><font style="color:#DF2A3F;">目前描述的并不是系统所有的功能，所有功能请看系统实现部分）</font>

## 2.1用户
1. 登录注册功能：用户可以通过账号，密码，邮箱，联系方式等信息进行注册账号，并通过注册的账

号进行登录系统。

2. 查看活动功能：用户可以查看活动类型，通过活动类型筛选活动信息，查看活动的详情信息，包含

活动的地点和参加过该活动的评价信息。

3. 活动预约功能：用户可以查看活动，对于喜欢的活动，可以进行预约。选择对应的日期和时间段，

进行预约。

4. 我的预约功能：用户可以查看自己预约的所有活动信息。可以进行取消预约。当参加完活动后，可

以进行评价活动。

5. 个人中心功能：用户可以进行修改个人信息和密码。

## 2.2 管理员
1. 用户信息管理功能：管理员有权对用户信息进行增删改查导出操作。
2. 活动分类管理功能：管理员进行维护活动分类信息。
3. 活动列表管理：管理员可以创建新的 DIY 手工活动，对已有的活动信息进行修改，当活动取消或

过期时，管理员可将其从活动列表中删除。

4. 活动评价管理：管理员可以查看所有用户对活动的评价内容，对于不友好的活动评价有权删除。
5. 活动图形化分析：环形图展示活动类型分布，饼状图展示活动评分分布，折线图展示近 7 天活动浏

览趋势。玫瑰图展示预约状态分布。横向柱状图展示热门活动 TOP5。

6. 预约配置管理：管理员可以设置预约的规则，如预约的开始时间、结束时间等，活动变动时，进行

及时变更。

7. 预约统计分析：系统通过环形图展示预约状态分布，柱状图展示每周预约分布，时段分布。折线图

展示月度预约趋势，饼状图展示用户分析。

8. 封面管理；管理员可以上传适合的图片作为系统的封面。

# **<font style="color:#48b378;background-color:#ffffff;">三.系统实现（部分截图）</font>**
## 3.1**登录注册功能的实现**
### 3.1.1**注册功能的实现**
用户注册账号，输入账号，密码，邮箱，联系方式，姓名，并输入图形验证码，进行注册。注册成功后，角色默认是用户角色。前端会跳转界面到登录界面，进行登录系统，操作系统。注册功能页面图如图5-1所示。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231395836-4834c17e-cfdc-4987-b477-3952f5d62c93.png)



注册功能模块具体的核心代码如下：

```java
//检查用户名是否存在
 			
Long userCount = AppUserMpper.selectCount(Wrappers.<AppUser>lambdaQuery()
 			
.eq(Extension.isNotNullOrEmpty(input.getUserName()),AppUser::getUserName, input.getUserName()));
 			
if (userCount > 0) {
 			
throw new CustomException("该用户名已经存在!");
 			
}
 			
//检查邮箱是否存在
 			
Long emailCount = AppUserMpper.selectCount(Wrappers.<AppUser>lambdaQuery()
 			
.eq(Extension.isNotNullOrEmpty(input.getUserName()),AppUser::getEmail, input.getEmail()));
 			
if (emailCount > 0) {
 			
throw new CustomException("该邮箱已经存在!");
 			
}
 			
//检查手机号是否存在
 			
Long phoneCount = AppUserMpper.selectCount(Wrappers.<AppUser>lambdaQuery()
 			
.eq(Extension.isNotNullOrEmpty(input.getPhoneNumber()), AppUser::getPhoneNumber, input.getPhoneNumber()));
 			
if (phoneCount > 0) {
 			
throw new CustomException("该手机号已经存在!");
 			
}
 			
return CreateOrEdit(input);
```

### 3.1.2**登录功能的实现**
用户登录系统，输入已注册的账号、密码进行登录，选择自己的角色身份进行登录，并输入图形验证码进行登录。登录成功后，进入系统首页界面。登录功能页面图如图5-2所示。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231400048-979f8a0e-a386-48cc-926f-5e24f119a074.png)

登录功能模块具体的核心代码如下：

```java
LambdaQueryWrapper<AppUser> queryWrapper = Wrappers.<AppUser>lambdaQuery()
 			
.eq(Extension.isNotNullOrEmpty(input.getUserName()),AppUser::getUserName, input.getUserName()).eq(Extension.isNotNullOrEmpty(input.getPassword()),AppUser::getPassword, input.getPassword()).eq(input.getRoleType() != null, AppUser::getRoleType, input.getRoleType());
 			
List<AppUser> items = AppUserMpper.selectList(queryWrapper);
 			
if (items.stream().count() == 0) {
 			
throw new CustomException("请检查登录的账号或者密码,角色是否都正确!");
 			
}
 			
Map<String, String> map = new HashMap<>();
 			
map.put(SysConst.UserIdClaim, items.get(0).getId().toString());
 			
map.put(SysConst.RoleTypeClaim, items.get(0).getRoleType().toString());
 			
String token = JWTUtils.getToken(map);
 			
return token;
```

## 3.2**活动信息功能的实现**
用户进入系统首页，可以通过活动类型筛选活动信息。活动列表采用卡片方式展示，能让用户一目了然地获取每个活动的关键信息。包含展示活动的创建时间，浏览次数，预约次数，评价量以及活动地址等信息。活动列表功能页面图如图5-3所示。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231406011-e176a2a4-22ca-442c-b64e-1de504bbdbea.png)

管理员可以进行管理活动列表信息，管理员可根据实际业务需求，添加新的活动信息，包含活动分类，活动标题，活动封面，活动的具体位置，活动内容等信息。若已有的活动信息发生变更，活动时间调整、地点更改或者活动内容更新等，及时进行调整。当活动不再运营时，管理员要删除活动信息。活动管理功能页面图如图5-4所示。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231408718-6da74e78-6759-4922-9782-55a11f2bdb70.png)

活动信息功能模块具体的核心代码如下：

```java
			
// 按创建时间从大到小排序 最新的显示在最前面
 			
queryWrapper = queryWrapper.orderByDesc(Activity::getCreationTime);
 			
// 构建一个分页查询的model
 			
Page<Activity> page = new Page<>(input.getPage(), input.getLimit());
 			
// 从数据库进行分页查询获取活动数据
 			
IPage<Activity> pageRecords = ActivityMapper.selectPage(page, queryWrapper);
 			
// 获取所有满足条件的数据行数
 			
Long totalCount = ActivityMapper.selectCount(queryWrapper);
 			
// 把Activity实体转换成Activity传输模型
 			
List<ActivityDto> items = Extension.copyBeanList(pageRecords.getRecords(), ActivityDto.class);
 			
DispatchItem(items);
 			
// 返回一个分页结构给前端
 			
return PagedResult.GetInstance(items, totalCount);
```

## 3.3**活动预约功能的实现**
用户查看活动列表，对于吸引到自己的活动信息，用户只需点击，便能进入该活动的详情界面。查看活动可以预约的时间，用户可根据自己的需求进行预约，填写手机号和姓名进行预约。预约成功后，用户可在“我的预约”界面进行查看。活动预约功能页面图如图5-5所示。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231413928-8cc86f38-7cc0-422b-8f4c-7c0eae7fb57a.png)

管理员能够依据活动筹备情况进行设置活动基本配置。包含活动的开始时间段，结束时间段以及有效时间。当活动时间有所变动，管理员要及时的进行更新，防止用户跑空。对于不再开展的时间段，管理员要进行删除。活动预约配置功能界面图5-6所示。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231527627-615da3ec-1de7-4a63-9bdb-9f6882c2a749.png)

活动预约配置功能模块具体的核心代码如下：

```java
List<AppointSetting> AppointSettings = AppointSettingMapper.selectList(Wrappers
 			
.<AppointSetting>lambdaQuery().eq(AppointSetting::getActivityId, input.getActivityId()));
 			 			
// 判断items在数据库中是否存在开始时间和结束时间之间的交集数据
 			
for (AppointSetting item : AppointSettings) {
 			
if (item.getId() != input.getId()) {
 			
if (!(input.getEndTime().isBefore(item.getBeginTime())
 			
|| input.getBeginTime().isAfter(item.getEndTime()))) {
 			
throw new CustomException("时间段发生冲突");
 			
}
 			
}
 			
}
```

## 3.4**活动统计功能的实现**
系统通过Echarts进行设计了一个活动相关的数据图形化分析界面，通过环形图展示不同类型活动的占比情况。帮助管理员了解各类活动的数量占比情况。以饼图呈现活动评分的分布状况，可以了解到哪些活动最受人们的喜爱。用折线图展示近7天的活动预约情况。横轴是日期，纵轴是预约量，折线反映预约量随时间的变化趋势。活动统计功能页面图如图5-7所示。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231481625-82128c3d-57c1-4b54-a78f-1e16ac19447c.png)

活动统计功能功能模块具体的核心代码如下：

```java
<!-- 图表区域 -->
 			
<el-row :gutter="20" class="chart-row">
 			
<el-col :span="12">
 			
<el-card>
 			
<div class="chart-title">活动类型分布</div>
 			
<div class="chart" id="typeChart"></div>
 			
</el-card>
 			
</el-col>
 			
<el-col :span="12">
 			
<el-card>
 			
<div class="chart-title">活动评分分布</div>
 			
<div class="chart" id="scoreChart"></div>
 			
</el-card>
 			
</el-col>
 			
</el-row>
```

## 3.5**我的预约功能实现**
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231521116-32bc4458-b455-4c9e-8e29-003e6029718e.png)

## **3.6手工课程功能实现**
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231455474-a1f784f6-4fa9-43f6-ba30-c3a23178b583.png)

## **3.7我的收藏功能实现**
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231541621-7c428e03-3f85-4ef7-83d6-f8f8dc11a14d.png)

## 3.8**预约设置管理功能实现**
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231496047-8065c908-cb05-480c-af64-3aec4b1487af.png)

## **3.9 预约统计功能实现**
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231466352-16153acf-90ab-449d-9f16-e40d6379a0b2.png)

## 3.10 **视频课程管理功能实现**
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231511721-1cad11f8-725e-47b6-a21a-28b502ff296a.png)

## 3.11 **课程统计功能实现**
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231506448-136a7302-a8cd-429d-bb52-7a43ffa534b5.png)

# **<font style="color:#48b378;background-color:#ffffff;">四.系统结构截图</font>**
## <font style="color:#48b378;background-color:#ffffff;">4.1后端</font>
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231488445-f7812e8b-14be-42a5-9c1c-855a5f46e048.png)

## <font style="color:#48b378;background-color:#ffffff;">4.2前端</font>
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231460487-bf3527e0-37ea-4095-b7fa-d2798814a36b.png)

## <font style="color:#48b378;background-color:#ffffff;">4.3数据库</font>
<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/png/45326128/1761231438190-f85177d9-58ee-466b-b1f5-8b003b5f5836.png)

# <font style="color:rgb(72, 179, 120);">五.</font><font style="color:rgb(26, 173, 25);">系统源码获取</font>
<font style="color:rgb(0, 0, 0);">1.系统非商用，非开源，非无偿。</font>

<font style="color:rgb(0, 0, 0);">2.由本人开发，非简单增删改查操作，业务逻辑完整。</font>

<font style="color:rgb(0, 0, 0);">3.项目有很多，并未全部上传，如果未找到想要的，可直接咨询。</font>



  


