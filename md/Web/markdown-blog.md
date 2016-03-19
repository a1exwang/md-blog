# 使用Markdown+git写Blog

- tags: web, ruby, wordpress

* * *

1. 需求
  - 使用markdown写blog
    1. markdown和html互相转换
    1. markdown中的相对地址自动转换为blog服务器上的url
    1. markdown中图片能自动上传到blog服务器
  - 一键从github同步到blog服务器
  - 可扩展

1. 思路
  - wordpress提供blog服务
  - 用wordpress REST API创建/修改posts
  - 用redcarpet做markdown到html的转换
    - 定制redcarpet, 在转换时修改url
  - 用wordpress钩子?/回调?钩住修改posts的动作, 将markdown同步到git上
