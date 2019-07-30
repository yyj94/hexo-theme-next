## hexo-theme-next
使用 hexo 搭建的静态博客

### 安装依赖
```bash
   $ npm i
```

### 本地运行
```bash
   $ hexo s
```

### 生成静态网页文件
```bash
   $ hexo g
```

### 清空生成目录
```bash
   $ hexo clean
```

### 在 GitHub Page 上部署发布
1. 新建一个仓库，命名为 'git用户名'.github.io，需要设置为公开
2. 修改源目录下 _config.yml 文件  
    ```
   deploy:
      type: git
      repo: https://github.com/yyj94/yyj94.github.io.git （GitHub Page 仓库地址）
      branch: master
   ```
3. 部署到远程
   ```bash
   $ hexo d
   ```

### 清洁部署
```bash
   $ hexo clean
   $ hexo g -d
```