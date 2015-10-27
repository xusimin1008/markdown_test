# 问答路由设计 #
```
全部问答： Route::get('ask', 'AskController@getIndex');
课程下的问答： Route::get('ask/lesson/{lesson_id}/questions', 'AskController@getLessonQuestions');
---------------------
某个问题：Route::get('ask/question/{quesiton_id}', 'AskController@getQuestion');

新建课程无关问题：Route::get('ask/question/new', 'AskController@getQuestionNew');
提交新建课程无关问题：Route::post('ask/question/new', 'AskController@postQuestionNew');

新建课程有关问题：Route::get('ask/lesson/<lesson_id>/question/new', 'AskController@getQuestionNew');
提交新建课程有关问题：Route::post('ask/lesson/<lesson_id>/question/new', 'AskController@postQuestionNew');

问题编辑：  Route::get('ask/question/{quesiton_id}/edit', 'AskController@getQuestionEdit');
提交问题编辑：Route::get('ask/question/{quesiton_id}/edit', 'AskController@postQuestionEdit');
---------------------
回答问题： Route::get('ask/question/{quesiton_id}/answer/new', 'AskController@getAnswerNew');
提交回答问题： Route::post('ask/question/{quesiton_id}/answer/new', 'AskController@postAnswerNew');

答案编辑： Route::get('ask/answer/<answer_id>/edit', 'AskController@getAnswerEdit');
提交答案编辑：Route::get('ask/answer/<answer_id>/edit', 'AskController@postAnswerEdit');
```
