# Rails Controller 简介

1. Controller 是什么？
2. Route 是什么？
3. Controller 与 Routes 基本 RESTful 请求的使用方式
4. RESTful 之外的请求如何添加。

## Controller 是什么？

Controller 全称是 Action Controller，是 MVC 中的"C"。

路由将请求转发给 Controller 中对应的 Action，而后由 Controller 中的各个 Action 对相应请求进行处理并作出反馈。

## Routes 与 Action 的对应关系

上面说到，路由将会把请求转发给 Controller 中对应的 Action。那么路由是什么？它与 Action 又是如何对应的呢？

|HTTP Verb|Path|Controller#Action|Used for|Helper|
|---------|----|-----------------|--------|
|GET|/photos|photos#index|display a list of all photos|
|GET|/photos/new|photos#new|return an HTML form for creating a new photo|
|POST|/photos|photos#create|create a new photo|
|GET|/photos/:id|photos#show|display a specific photo|
|GET|/photos/:id/edit|photos#edit|return an HTML form for editing a photo|
|PATCH/PUT|/photos/:id|photos#update|update a specific photo|
|DELETE|/photos/:id|photos#destroy|delete a specific photo|

其中所有 GET 请求对应的 Action 都有相应视图。
