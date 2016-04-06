# Xiahl1990_LearningResource
github上值得关注的前端项目:http://segmentfault.com/a/1190000002804472

jQuery代码最佳实践：http://gregfranko.com/jquery-best-practices/

在Sublime Text 3中配置编译和运行Java程序:http://www.open-open.com/lib/view/open1388105023765.html

前端从小白到大神必读资料汇总:http://www.cnblogs.com/jason-swift/archive/2016/01/26/5159744.html


---------------Begin AngularJS-------------------

中文学习资料：
中文资料且成系统的就这么多，优酷上有个中文视频。

https://segmentfault.com/a/1190000003761054   关于Angular2的一些资料（持续更新中）

http://www.cnblogs.com/lcllao/archive/2012/10/18/2728787.html   翻译的官方的Guide

http://www.ituring.com.cn/minibook/303  翻译的官方的tutorial

http://www.lovelucy.info/angularjs-best-practices.html  Angular最佳实践

http://zouyesheng.com/angular.html  angularjs的学习笔记

http://www.sunzhongwei.com/angularjs.html 另一个网友的笔记

https://github.com/basestyle/angularjs-cn  "AngularJS"中译本 -《AngularJS》

https://github.com/jmcunningham/AngularJS-Learning/blob/master/CN-CN.md  github上的一个资料整理

工具：
AngularJS WebInspector Extension for Chrome

https://github.com/yeoman/generator-angular   YeoMan的帮助创建angularjs APP

https://github.com/johnlindquist/angularjs-plugin 适合Idea、WebStorm等Intellij平台的IDE插件

https://github.com/angular-ui/AngularJS-sublime-package  Angularjs的Sublime插件

库：
http://angular-ui.github.io/  AngularUI - The companion suite for AngularJS

http://twilson63.github.io/ngUpload/  上传文件的指令

http://binarymuse.github.io/ngInfiniteScroll/ 无限下拉

https://github.com/btford/angular-dragon-drop  拖拽的指令

 

Demo：
可以参考参考怎么组织代码

https://github.com/tastejs/todomvc   帮助你选择MV* 框架，其中有一个angularjs的demo

https://github.com/yearofmoo-articles/AngularJS-Animation-Article 

https://github.com/zensh/jsgen  angularjs+nodejs开发的一套社区软件

https://github.com/btford/angular-express-seed angularjs + express 骨架，想用这两者结合开发的可以参考下怎么组织代码结构

https://github.com/btford/angular-express-blog 用上面的框架写的一个简单的Blog系统

https://github.com/bennadel/AngularJS-Routing AngularJS - Deep Routing Example

https://github.com/GoogleChrome/wReader-app  RSS Reader written using AngularJS

https://github.com/btford/angular-socket-io-im  angular + socket.io 开发的简单的Demo

https://github.com/saberma/19wu 19屋源码 rails + angularjs

---------------End AngularJS-------------------


--------------Begin 资源搜索网站------------------

cdnjs.com 
http://www.aseoe.com/api-download/download.html  爱思资源网，各种API下载

--------------End 资源搜索网站--------------------


-----------------例子----------------

<!doctype html>
<html>
<head>
	<meta charset="utf-8">
    <title>test</title>
    <link rel="stylesheet" type="text/css" href="components/Semantic-UI-master/dist/semantic.css">

    <script type="text/javascript" src="src/angular2-polyfills.js"></script>
    <script type="text/javascript" src="src/system.js"></script>
    <script type="text/javascript" src="src/typescript.js"></script>
    <script type="text/javascript" src="src/Rx.js"></script>
    <script type="text/javascript" src="src/angular2.dev.js"></script>
    <script type="text/javascript" src="src/http.dev.js"></script>
    <script type="text/javascript" src="src/router.dev.js"></script>
    <script type="text/javascript" src="src/tsloader.js"></script>
    <script type="text/javascript" src="src/system.config.js"></script>
    <script type="text/javascript" src="components/jquery/jquery.min.js"></script>
    <script src="components/Semantic-UI-master/dist/semantic.js"></script>
    <!-- <script type="text/javascript" src="dist/angular2.beta.stack.min.js"></script> -->
</head>
<body>
	<ez-app></ez-app>
    <script type="text/typescript">
    	import {Component} from "angular2/core";
        import {bootstrap} from "angular2/platform/browser";

        class Article { 
            title: string; 
            link: string; 
            votes: number;
            constructor(title: string, link: string, votes?: number) {
                this.title = title;
                this.link = link;
                this.votes = votes || 0;
            }
            voteUp(): void { 
                this.votes += 1;
            }
            voteDown(): void { 
                this.votes -= 1;
            }
            domain(): string { 
              try {
                const link: string = this.link.split('//')[1];
                return link.split('/')[0]; 
              } catch (err) {
                  return null;
              }
            }
        }


        @Component({
            selector:"ez-article",
            inputs: ['article'],
            host:{
              class:'row'
            }
            template: `
            <div class="four wide column center aligned votes">
                <div class="ui statistic">
                    <div class="value"> {{ article.votes }}
                    </div>
                    <div class="label">
                        Points
                    </div>
                </div>
            </div>
            <div class="twelve wide column">
                <a class="ui large header" href="{{ article.link }}"> {{ article.title }}
                </a>
                <div class="meta">({{ article.domain() }})</div>
                <div class="ui big horizontal list voters">
                    <div class="item">
                        <a href (click)="voteUp()">
                            <i class="arrow up icon"></i> upvote
                        </a>
                    </div>
                    <div class="item">
                        <a href (click)="voteDown()">
                            <i class="arrow down icon"></i>
                            downvote
                        </a>
                    </div>
                </div>
            </div>
            `
        })  
        class ArticleComponent { 
          article: Article;
          voteUp(): boolean {
            this.article.voteUp();
            return false;
          }
          voteDown(): boolean { 
            this.article.voteDown(); 
            return false;
          }
        }


        @Component({
			selector:"ez-app",
            directives: [ArticleComponent],
        	template : `
            <div class="ui top segment">
                <form class="ui form ">
                    <h3 class="ui header">Add a Link</h3>
                    <div class="field">
                        <label for="title">Title:</label> 
                        <input name="title" #newtitle>
                    </div>
                    <div class="field">
                        <label for="link">Link:</label>
                        <input name="link" #newlink>
                    </div>
                    <button (click)="addArticle(newtitle, newlink)" class="ui positive button">
                        Submit link
                    </button>
                </form> 
            </div>
            <div class="ui grid posts">
              <ez-article
                *ngFor="#article of sortedArticles()"
                [article]="article">
              </ez-article>
            </div>
                `
        })
        class EzApp{
            articles: Article[];
            constructor() {
                this.articles = [
                  new Article('Angular 2', 'http://angular.io', 1),
                  new Article('Fullstack', 'http://fullstack.io', 2),
                  new Article('Angular Homepage', 'http://angular.io', 3),
                ]; 
            }
            addArticle(title: HTMLInputElement, link: HTMLInputElement): void { 
                console.log(`Adding article title: ${title.value} and link: ${link.value}`);
                this.articles.push(new Article(title.value, link.value, 0));
                title.value = '';
                link.value = '';
            }
            sortedArticles(): Article[] {
                  return this.articles.sort((a: Article, b: Article) => b.votes - a.votes);
            }
        }
        
        bootstrap(EzApp);
    </script>
</body>
</html>
