# markdown_test

## 二级标题

### 三级标题

1. 有序条目1
2. 有序条目2
3. 有序条目3
4. 有序条目4

* 无序条目1
* 无序条目2
* 无序条目3

这是[链接测试](http://www.baidu.com)

>这是块区间元素测试
> 
>再测试一下

    这是一个代码区块。

***

**字体加粗测试**
## Markdown 学习笔记 ##
1. Setext 形式是用底线的形式，利用 = （最高阶标题）和 - （第二阶标题），
	Atx 形式在行首插入 1 到 6 个 # ，对应到标题 1 到 6 阶。	
> **行首的井字符数量决定标题的阶数**

2. 块引用是使用类似 email 中用 > 的引用方式。

3. 无序列表使用星号、加号或是减号作为列表标记。
有序列表则使用数字接着一个英文句点
> **有序和无序都要在标记后面加一空格， 否则不能生效**

4. 代码区块缩进4个空格或是1个制表符。

可查看[Markdown 语法说明 (简体中文版)](	https://gitcafe.com/riku/Markdown-Syntax-CN/blob/master/syntax.md)

***

## 创建新的larvel项目 ##
1. 使用命令：laravel new project_name
2. 修改homestead的site map （在.homestead下的Homestead.yaml）
3. 修改host里面的主机映射（在.homestead下的hosts）


***
## vagrant操作事项：##
1. 连接到vagrant： vagrant ssh
2. 查看状态： vagrant status
3. 创建项目时需要重启环境：vagrant provision


***
## github操作事项 ##
1. 先从主干fork一份到自己仓库
2. 从自己仓库clone一份到本地
3. 提交修改到本地
4. pull request到远端
5. 注意同步更新本地代码


***
## Laravel5学习事项 ##
1. LV中页面提交form表单，需要设置{{ csrf_token() }}.
	### Routing ###
	1. Route:: + http_method(path, Closure); 注册一种路由请求
	2. Route::match(['get', 'post'], '/', function(){}); 注册多种路由请求
	3. Route::any('/', function(){}); 注册全部路由请求
	4. Route::get('user/{id}', function($id)
		{
		    return 'User '.$id;
		}); 基础路由参数
	5. Route::get('user/{name?}', function($name = null)
		{
		    return $name;
		}); 可选择的路由参数
	6. Route::get('user/{name}', function($name)
		{
		    //
		})
		->where('name', '[A-Za-z]+'); 使用正则表达式限制参数


	### Middleware ###
	1. LV默认包含了一个中间件来检验用户身份验证，如果用户没有经过身份验证，中间件会将用户导向登录页面；
	2. 在项目路径下执行：php artisan make:middleware MiddlewareName；
	3. 全局中间件：中间件的类加入到 app/Http/Kernel.php 的 $middleware 属性清单列表中；
	   指派中间件给特定的路由，你得先将中间件在 app/Http/Kernel.php 的 $routeMiddleware 配置一个键值。
	4. 创建中间件 ＝> 注册中间件

	### Views ###
	1. 视图对应的文件夹目录是：resources/views， 其内的子文件夹,如视图文件保存在 resources/views/admin/profile.php，你可以用以下的代码来返回：return view('admin.profile', $data);
	
	
	### Cache ###
	1. 缓存配置文件位在 config/cache.php,默认使用文件缓存系统


	### Localization ###
	1. 语言字串保存在 resources/lang 文件夹的文档里;
	2. 在执行时变换默认语言: App::setLocale('es');
	3. 配置备用语言: 'fallback_locale' => 'en';
	4. Lang::get('messages.welcome'); <=> trans('messages.welcome');

	### Errors & Logging ###
	1.要让所有的 404 错误返回自定义的视图，请建立一个 resources/views/errors/404.blade.php 文件。(其他的错误类似)
	2. LV默认为应用程序建立每天的日志文件在 storage/logs 目录。

	### Mail ###
	1. 邮件配置文件为 config/mail.php
	2. 基本用法: Mail::send('emails.welcome', ['key' => 'value'], function($message)
				{
				    $message->to('foo@example.com', 'John Smith')->subject('Welcome!');
				    $message->attach($pathToFile);  添加附件
				});
	3. 邮件队列: Mail::queue('emails.welcome', $data, function($message)
				{
				    $message->to('foo@example.com', 'John Smith')->subject('Welcome!');
				});
	4. 指定邮件队列:Mail::queueOn('queue-name', 'emails.welcome', $data, function($message)
				{
				    $message->to('foo@example.com', 'John Smith')->subject('Welcome!');
				});

	### Pagination ###
	1. DB::table('users')->paginate(15); 对应于Illuminate\Pagination\LengthAwarePaginator， 有显示页书和上下页;
	2. User::where('votes', '>', 100)->simplePaginate(15); 对应于Illuminate\Pagination\Paginator， 只是简单显示上下页;
	3. 分页的显示需要引入bootstrap.css，在.blade.php 中{!! $users->render() !!}显示;
	4. 追加分页链接， {!! $users->appends(['sort' => 'votes'])->render() !!};
	5. 追加哈希片段，{!! $users->fragment('foo')->render() !!};
	6. 直接返回其值，就是返回JSON数据格式。

	### Session ###
	1.session 的配置文件配置在 config/session.php 中, 默认使用 file 的 session 驱动
	2.有时你可能希望暂存一些数据，并只在下次请求有效。你可以使用 Session::flash 方法来达成目的

	### Eloquent ORM ###
	> _这部分以下的代码只是起演示作用，具体用法以官方文档为主_
	
	1. Relationships
		1. 一对一
			1. return $this->hasOne('App\Phone', 'foreign_key', 'local_key');
			2. return $this->belongsTo('App\User', 'local_key', 'parent_key');
		2. 一对多
			1. return $this->hasMany('App\Comment', 'foreign_key', 'local_key');
			2. return $this->belongsTo('App\Post', 'local_key', 'parent_key');
		3. 多对多
			1. 多对多关联需要用到三个数据库表， 比如： users ， roles ，和 role_user
			2. return $this->belongsToMany('App\Role', 'user_roles', 'user_id', 'foo_id');
			3. 2. return $this->belongsToMany('App\User', 'user_roles', 'user_id', 'foo_id');
		4. 远层一对多关联（可以经由多层间的关联取得远层的关联）
			1. countries
				    id - integer
				    name - string

				users
				    id - integer
				    country_id - integer
				    name - string

				posts
				    id - integer
				    user_id - integer
				    title - string
			2. return $this->hasManyThrough('App\Post', 'App\User', 'country_id', 'user_id');
		5. 多态关联（让一个模型同时关联多个模型）
			1. return $this->morphTo();
			2. return $this->morphMany('App\Photo', 'imageable');	
		6. 多态的多对多关联
			1. return $this->morphToMany('App\Tag', 'taggable');
			2. return $this->morphedByMany('App\Post', 'taggable');
			3. return $this->morphedByMany('App\Video', 'taggable');

	### 注意细节 ###
	1. 页面尽量都以blade.php来写
	2. 路由配置尽量和Controller里面的方法一一对应，不需要放在一起
	3. 数据库操作尽量都以Eloquent ORM来进行（不需要在数据库表中建立外键关系）

	#### 问题列表 ####
	1. 尝试了一下LV的分页实现，不过并不是异步加载，想了解一下如何通过JS异步加载数据
	2. php页面中涉及判断，如何分别展现html代码和php代码
	3. 一些后台数据的打印在哪里查看（后端调试）
	4. 如何使用sequel建立关联表
	5. 比方像redirect()，怎么知道里面有什么方法
	6. 使用ORM，数据库的表必须包含updated_at，created_at两个字段？

### 注意事项 ###
1. 注意切换到_**指定版本和环境**_下, 比方在虚拟环境下我的virtualenv在/home/vagrant/python中



windows下python环境集成:http://continuum.io/downloads#all


