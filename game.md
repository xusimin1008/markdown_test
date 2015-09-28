1. [doubiliving](http://msgjug.com/p_life/page.html)
2. stackoverflow: qq email: Leslie1008
3. pipy: qq email: night1008lslie1008
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
	或者（推荐）composer create-project laravel/laravel test-laravel-5-project --prefer-dist 
2. 修改homestead的site map （在.homestead下的Homestead.yaml(cd ~/.homestead)）
3. 修改host里面的主机映射（在/etc下的hosts）


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
2. 在Linux下 . 和 source 的作用相同 
3. 有些文件如果不想提交，可以在.gitignore里面进行添加路径和文件名
4. linux解压： tar zxvf node-v0.6.1.tar.gz 
5. 删除进程： ps ax | grep -v grep | grep process_name | awk '{print $1}' | xargs kill
6. 启动mysql服务：sudo service mysql start
7. ssh user@host
8. 显示内存使用情况: cat /proc/meminfo

### 查看虚拟机下nginx下启动了哪些程序 ###
cd /etc/nginx/sites-available/

### 虚拟机下主机映射 ###
subl /etc/hosts(添加地址映射)

### 数据库迁移 ###
php artisan migrate(在项目目录下)

### 可以使用国内的pip源 ###
pip install --trusted-host pypi.mirrors.ustc.edu.cn -i http://pypi.mirrors.ustc.edu.cn/simple/ {包名}

### mysql学习 ###
1. 查看某个表的索引: SHOW INDEX FROM yourtable;

### Laravel 测试 ###
_由于想用laravel自带的phpunit命令进行测试，出现了权限问题，所以换用另一种方式_
1. wget https://phar.phpunit.de/phpunit.phar (在项目目录下执行)
2. php phpunit.phar

### Laravel debugger学习 ###
1. 安装
	1. 在项目目录下执行: composer require barryvdh/laravel-debugbar
	2. 到config/app.php文件中, providers配置下添加Barryvdh\Debugbar\ServiceProvider::class,
		aliases配置下'Debugbar' => Barryvdh\Debugbar\Facade::class,
	3. php artisan vendor:publish
	4. 如有必要可进行缓存和配置缓存清除:
		1. php artisan cache:clear 
		2. php artisan config:clear
2. 使用：
	1. 可以在View中或Controller写入调试代码，比如:
	<?php Debugbar::info(‘Debug'); ?>
	就可以在浏览器端看到调试条了。


### 关联规则 ###
_以下D代表一个数据集合_
1. 数据离散化 => 找出高频项目组 ＝> 产生关联规则，
2. 找出高频项目组: 对D中的所有元素进行组合，需要满足指定支持度
3. 产生关联规则:  对各种组合进行计算，验证是否满足给定的支持度和可信度，
4. 假设要计算 X->Y 是否在D中的存在关联规则，
5. 关联规则在D中的支持度(support)是D中事务同时包含X、Y的百分比，即概率，
6. 置信度(confidence)是D中事务已经包含X的情况下，包含Y的百分比，即条件概率，
7. 如果满足最小支持度阈值和最小置信度阈值，则认为是有关联的。

### 安装gensim ###
1. 先安装其依赖 NumPy and Scipy
	1. 安装Numpy: 由于之前安装Pandas时顺带安装了，如果独立安装，需再找一下。
	2. 安装[Sccipy](https://github.com/scipy/scipy/blob/master/INSTALL.rst.txt#id8):
	sudo apt-get install python python-dev libatlas-base-dev gcc gfortran g++
2. 运行: pip install -U gensim

### git flow 在 sourcetree上的使用 ###
_以下我们把远端原始的项目库叫**main**， fork了别人的代码库叫**master**，克隆到本地的代码库叫**develop**_
1. 首先到github的项目main fork一份自己的远端代码master
2. 克隆自己的远端代码到本地
3. 在自己本地代码的基础上创建分支develop
4. 在自己的scourcetree上的REMOTES分别克隆远端的master和main代码库，
5. 如果做修改：
	1. 提交修改到本地分支
	2. push到远端main，也就是pull－request，等待项目管理员审核
6. 如果做更新（拉取最新代码）:
	1. 同时需要更新develop和master代码库(注意分支之间的对应)

### datartery项目学习 ###
	#### 产品问题 ####
	1. 商品的好坏和评论有关，也和销量有关，像我网购一般选的是销量高和评论好的，但是如果只依赖评论是否过于片面？
	2. 用户是有地区的，是否可以提供用户的地区分布？
	3. 商品是有上架时间的，是否可以提供商品销售时间分布？
	4. 商品的促销途径是否对商品增加销量有益？
	5. 商品本身的款式不同，是否可以提供各款式的销量分布？
	6. 商品的评论时间和购买时间是不一致的，那么语料时间分布的意义是否会减小？
	7. 对于商品评论的评论或其支持数，反对数如何处理？

	#### 实现问题 ####
	1. 原数据（meta）里面存储的说什么？
	2. 数据来源中表格压缩（页面展示）
	3. 数据的获取方式的怎么样多，同步或异步？
	4. 评论是不断在更新的，那么我们要怎么同步更新？
	5. corpus_product这个表时用来干什么的？
	6. 数据库中的item_id从哪里来？
	7. 语料分析通过什么途径或方法？
	8. 大都页面都是需要搜索和排序的
	9. 主题分析页面是否不应该能左右滑动？
	10. 测试数据源抓取失败，为何？（亚马逊书籍抓取） －－没开抓取进程
	11. 简单概述下scrapy的抓取流程 
	12. 每次parse页面的时候都有yield，才能经过pineline

	13. 联系我们页的反馈信息不应该跳到首页，还有位置问题。
	14. 订阅和以上有同样的问题，且对于已经订阅的没有提示， 还有订阅是如何推送的？
	15. celery-flower api封装的错误处理。
	16. analysis中 计算项目语料的词频 一定已经有analysis对象了？
	17. jieba分词的全模式和搜索引擎模式有什么区别？
	18. pd.Grouper(freq='1M', key='pubdate') 中的freq＝'1M' 是什么意思
	19. run_group_source_count中对dfc_source_date的处理是干什么？
		=> 本来是： {(pubdate, source_id): count} 变成 {pubdate: (source_id, count)}

	20. run_group_count和run_group_source_count是否有重复？
		＝> 想获得某个项目的词料数目，是否可以把所有的源数目加起来？
	21. 词向量没看懂（深度学习）
	22. 我的Laravel是否也需要更新？


在git上fork一份代码库（里面包含已存在的分支）
git clone url （克隆远端代码库的master分支）
git checkout -b develop origin/master

git add －A caterory/ （添加指定目录的全部文件，同时删除已删除的文件）
git commit
到github上进行pull request(注意分支的对应，main的develop应该对应origin的develop)


### Laravel代码发生项目库启动错误 ###
1. 使用国内数据源: composer config -g repositories.packagist composer http://packagist.phpcomposer.com
2. rm -Rf vendor/ (删除项目库)
3. php composer.phar update -vvv

### 查看当前laravel的版本 ###
到composer.lock里面查看


### roclaws问题 ###
启动celery: python run_celery_worker.py somename

1. 项目内的爬虫可定时，是否在选择定时后用户可以选择时间？（这个定时作业是相对于用户的）
2. 用户怎么知道如何去写爬虫规则，可能用户有时候也不知道需要保存哪些网页？主要是如何达到让用户简单易用的目标？
3. 是否应该有保存网页内容的Model？｛base_url, self_url, content, spider_id ...｝
4. 分布式需要怎么做？


5. follow_pattern和save_pattern可能都有很多个，可用正则表达式的  ()｜()| ()
6. 数据存储格式说要怎么样
7. 用户的修改信息和密码设置是否有现成的东西可以用
8. celery scrapy 包引用问题
9. result结构 project_id, url
10. job status
11. spider time

12. 抓取的网页含有下一页或者下拉加载更多的是否也需要处理？
13. 关于任务定时，是在每隔一段时间就去检查有哪些定时job需要执行？这样是否会有遗漏？
14. 如果按照方案2 job里面的kwargs会重复保存，（因为job对应task，或者说就是）
15. 如果是定时，是否应该有一个计数器（task计数器不需要，展示的时候分组一下，按时间排序，添加一个序号即可）
16. 定时作业是否要设置一个结束时间？
17. result是否需要project_id?
18. 直接把celery task的任务ID当成数据库里面的ID是否适合？

### Migration过程 ###
1. 创建Model: php artisan make:model User
2. 创建迁移脚本: php artisan make:migration create_users_table
3. 往上步的create_users_table里面添加User定义的字段
4. 执行: composer dump-autoload
5. 执行: php artisan migrate (--seed)

### Test过程 ###
使用phpunit进行测试
1. phpunit tests/SomeTest


### git stash ###
1. 如果有uncommitted时，需要pull，则可以先stash，在git console内执行git stash
2. pull完成后中source tree上执行： STASHES apply

### phantomjs + selenium python ###
_在虚拟机环境下：_
1. sudo apt-get install phantomjs
2. pip install selenium


### postgresql ###
1. sudo -s (切换到虚拟系统的root用户)
2. su postgres(postgres是postgres数据库默认创建的系统用户)
3. psql (进入postgres数据库)
4. \password postgres (修改数据库密码)
5. CREATE USER dbuser WITH PASSWORD 'password'; (创建数据库用户dbuser并设置密码)
6. CREATE DATABASE exampledb OWNER dbuser; (创建用户数据库并指定所有者为dbuser)
7. GRANT ALL PRIVILEGES ON DATABASE exampledb to dbuser; (将exampledb数据库的所有权限都赋予dbuser)
8. psql -U dbuser -d exampledb -h 127.0.0.1 -p 5432 (登录数据库)
9. 用户名： xusimin 密码： xsm123456

### 项目测试 ###
1. spider_name: 163news
2. start_url: http://bj.house.163.com/special/bj_ztlist/
3. follow_pattern: http://bj.house.163.com/special/news_huayuanheshuyayuan/
4. save_pattern: http://bj.house.163.com/14/\d+/\d+/\w+\.html

1. 使用selenium的翻页问题(页脚也上异步加载的)

2. danel项目是干什么的
3. 事件驱动（数据驱动）要怎么理解，是分析其他网站的？
4. 每个事件驱动是不是伴随着用户驱动？匿名用户和登录用户需要辨别（uuid是否为空进行判断？） ＝》 事件里有用户标志
4. 配置一堆VPN地址，随机产生一个，如果这个可行，则后续的使用这个地址，如果不行，尝试几次后重新随机产生


5. properties为什么只能为单层（为以后操作方便？）
6. user驱动需要有uuid，那么匿名用户是否就遭废弃，匿名用户是否有用户驱动？
7. 这些事件，用户驱动的其实就是相当于日志的记录（AOP）
8. 以后在事件驱动里是否可以支持改名，或增删字段？
9. 为什么要保存两张表，ES and PG
apt-get install postgresql-9.4
tinyproxy
scrpay proxy

网站转化率=进行了相应的动作的访问量/总访问量
留存率=新增用户数/登录用户数*100%（一般统计周期为天）

用户未注册或登录时，使用cookieID辨别，一旦用户注册或登录，则通过trackSignUp进行关联，但是cookieID是否是可变的？
转化时间中位数是什么概念？
每个danel中的event和user的name都应该有一个对应的显示名称
有元事件和虚拟时间的概念
未登录或未注册用户登录，注册后需要关联
如何去构造灵活可用的sql查询
基本元素是event和与之关联的user，
有关于用户的总体概览，和对各个自定义event的概览
event借口都是trace(uuid,event,properties)
数据格式的验证
