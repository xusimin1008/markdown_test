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
2. 修改homestead的site map （在.homestead下的Homestead.yaml(cd ~/.homestead)）
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
			> 1. return $this->hasOne('App\Phone', 'foreign_key', 'local_key');
			> 2. return $this->belongsTo('App\User', 'local_key', 'parent_key');
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
	2. 关联查询
		1. $posts = Post::has('comments', '>=', 3)->get();
		2. $posts = Post::whereHas('comments', function($q)
					{
					    $q->where('content', 'like', 'foo%');

					})->get();
	3. 预载入
		1. 使用 with 方法指定想要预载入的关联对象,
			foreach (Book::with('author')->get() as $book)
			{
			    echo $book->author->name;
			}
	4. 新增关联模型
		1. 新增一个关联模型，$comment = $post->comments()->save($comment);
		2. $post->comments()->saveMany($comments);
		3. 新增从属关联模型，要更新 belongsTo 关联时，可以使用 associate 方法, $user->account()->associate($account);
		4. 新增多对多的关联模型, $user->roles()->attach(1, ['expires' => $expires]);
	5. 属性类型转换
		如果您想要某些属性始终转换成另一个数据类型, 您可以在模型中增加 casts 属性。
	6. 转换成数组 / JSON
		1. return User::find(1)->toJson();
		2. 转换成数组或 JSON 时隐藏属性,只要在模型里增加 hidden 属性即可

	### 注意细节 ###
	1. 页面尽量都以blade.php来写
	2. 路由配置尽量和Controller里面的方法一一对应，不需要放在一起
	3. 数据库操作尽量都以Eloquent ORM来进行（不需要在数据库表中建立外键关系）
	4. 生成URL的方法，$url = action('FooController@method');或者 $url = route('name');
	5. 在JS中获得php代码中的对象时，.blade.php页面中使用： json_encode($name) !!}
	6. .blade.php 和其他JS库，比如Vue.js一起使用时，变量要使用: @{{name}}

	#### 问题列表 ####
	1. 尝试了一下LV的分页实现，不过并不是异步加载，想了解一下如何通过JS异步加载数据
	2. php页面中涉及判断，如何分别展现html代码和php代码
	3. 一些后台数据的打印在哪里查看（后端调试）
	4. 如何使用sequel建立关联表
	5. 比方像redirect()，怎么知道里面有什么方法
	6. 使用ORM，数据库的表必须包含updated_at，created_at两个字段？
	7. 页面里面的form怎么填写比较规范？
	8. 怎么关联删除？比如删除一篇文章，也同时删除里面的评论
	9. 表单验证时只使用withInput()怎么不起作用？
	（在页面中使用{{ old('name') }}或者不使用redirect，直接使用back()->withInput()->withErrors($validator->errors()))
	10. 语料源与语料数据各是什么？
	11. 各个网站各个商品的信息和评论各不相同，需要怎么配置抓取路径？
	12. 可以在JS代码里面写php代码？
	13. 关闭shell是否可以直接关闭虚拟机？(是shell子进程，可以关闭)
	14. 如何查看mysql在什么位置？


### virtualenv学习 ###
具体使用都可查看［Virtual Environments］(http://docs.python-guide.org/en/latest/dev/virtualenvs/)

### Mac下启动redis ###
redis-server /usr/local/etc/redis.conf
(homestead下默认有安装redis)

### Vagrant启动 ##
到Homestead目录下运行 vagrant ssh


### celery and flower ###
1. 在指定环境下安装celery: pip install celery
2. 在制定环境下安装flower: pip install flower
3. 编写相关的celery任务，相关操作可查看：[First Steps with Celery](http://celery.readthedocs.org/en/latest/getting-started/first-steps-with-celery.html)
3. 启动celery和flower: 
	1. celery -A proj worker --loglevel=info
	2. celery flower -A proj --port=5555
4. 查看flower的相关调用： [flower REST API](http://nbviewer.ipython.org/github/mher/flower/blob/master/docs/api.ipynb)
5. 任务查看: 访问http://1localhost:5555/
6. 注意事项: (如果用虚拟环境配置的，则localhost对应多地址是虚拟地址，比如：192.168.10.10)

### 全局注意事项 ###
1. 注意切换到_**指定版本和环境**_下, 比方在虚拟环境下我的virtualenv在/home/vagrant/python中
