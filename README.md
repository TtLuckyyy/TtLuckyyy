<div align="center">
    <img src="https://capsule-render.vercel.app/api?type=waving&color=d91c25&height=260&section=header&text=NAME&fontSize=90&animation=fadeIn&fontAlignY=38&desc=%E5%90%BE%E5%8D%B3%E6%98%AF%E6%B1%9D%EF%BC%8C%E6%B1%9D%E5%8D%B3%E6%98%AF%E5%90%BE&descAlignY=55&descAlign=60"
        width="100%" />
</div>

## 👋 你好，我是Zixiang ！
**个人定位**

邮箱: [XXX.com](mailto:XXXX.com) &nbsp;&nbsp;|&nbsp;&nbsp; 

<p align="left">
    <img src="https://img.shields.io/badge/SwiftUI-d91c25?style=flat-square&logo=swift&logoColor=white" />
    <img src="https://img.shields.io/badge/iOS-000000?style=flat-square&logo=apple&logoColor=white" />
    <img src="https://img.shields.io/badge/Python-d91c25?style=flat-square&logo=python&logoColor=white" />
    <img src="https://img.shields.io/badge/Unity-000000?style=flat-square&logo=unity&logoColor=white" />
    <img src="https://img.shields.io/badge/Git-d91c25?style=flat-square&logo=git&logoColor=white" />
    <img src="https://img.shields.io/badge/MySQL-000000?style=flat-square&logo=mysql&logoColor=white" />
    <img src="https://img.shields.io/badge/Node.js-d91c25?style=flat-square&logo=node.js&logoColor=white" />
</p>

## 👨‍💻 关于我 

这里可以写一段简短的自我介绍，比如你正在学习什么，或者你在寻找什么样的合作机会。

name: generate animation

on:
  # run automatically every 2 hours
  schedule:
    - cron: "0 */2 * * *" 
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the master branch
  push:
    branches:
    - master
  
  

jobs:
  generate:
    permissions: 
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5
  
    steps:
      # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
  
  
      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
