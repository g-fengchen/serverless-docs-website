<template>
  <div class="home-feature py-10 px-10">
    <el-row :gutter="60">
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">无厂商锁定</p>
          <p class="text-sm">
            目前Serverless Devs 已经支持了
            <a href="https://github.com/devsapp/fc" target="blank"
              >阿里云函数计算</a
            >
            、
            <a href="https://github.com/devscomp/lambda" target="blank"
              >AWS Lambda</a
            >
            、
            <a href="https://github.com/xinwuyun/cfc" target="blank"
              >百度智能云函数计算</a
            >
            、
            <a href="https://github.com/xinwuyun/fg" target="blank"
              >华为云函数工作流</a
            >
            、
            <a href="https://github.com/devscomp/scf" target="blank"
              >腾讯云云函数</a
            >
            等多云的 FaaS 产品
          </p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">开源开放</p>
          <p class="text-sm">
            项目通过开源代码，开放生态进行建设的，开发者可以随时查看和参与
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs"
              target="blank"
              >Serverless Devs</a
            >
            开发者工具的贡献，也可以随时随地进行相关
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/package_dev.md#%E7%BB%84%E4%BB%B6%E5%BC%80%E5%8F%91%E8%AF%B4%E6%98%8E"
              target="blank"
              >组件</a
            >
            和
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/package_dev.md#%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91%E8%AF%B4%E6%98%8E"
              target="blank"
              >应用</a
            >
            的贡献。
          </p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">功能可插拔</p>
          <p class="text-sm">
            Serverless
            Devs工具本身并不具备任何业务能力，所有的业务能力均是通过组件化的形式，进行可插拔式使用。开发者可以在一个应用中，选择不同的组件完成对应的业务能力。
          </p>
        </div>
      </el-col>
    </el-row>

    <el-row :gutter="60" class="mt-8">
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">简单易用</p>
          <p class="text-sm">
            可以通过应用的模式，为开发者提供多种场景的上手案例。帮助开发者快速了解、学习、深入
            Serverless 架构，例如新手引导中的
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/quick_start.md#serverlesshello-world"
              target="blank"
              >Serverless：Hello World</a
            >
            、<a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/quick_start.md#%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%E7%9B%AE%E6%A0%87%E6%A3%80%E6%B5%8B"
              target="blank"
            >
              人工智能：目标检测
            </a>
            、
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/quick_start.md#%E4%BC%A0%E7%BB%9F%E6%A1%86%E6%9E%B6%E5%9F%BA%E4%BA%8Edjango%E7%9A%84%E5%8D%9A%E5%AE%A2%E9%A1%B9%E7%9B%AE"
              target="blank"
            >
              传统框架：Django博客项目
            </a>
            等
          </p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">应用全生命周期管理</p>
          <p class="text-sm">
            通过组件化的支持，Serverless Devs
            可以在应用的全生命周期发挥重要的作用，以
            <a href="https://github.com/devsapp/fc" target="blank"
              >阿里云函数计算的FC组件</a
            >
            为例，开发者可以在项目创建、项目的开发、调试、可观测性等多个层面进行项目的建设和管理
          </p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">良好的集成与被集成性</p>
          <p class="text-sm">
            可以通过组件化的支持，非常简单的与传统的生态进行有机结合。同时也可以非常简单的被集成到海量的自动化流程中，例如
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/cicd.md"
              target="blank"
              >CI/CD</a
            >
            文档中，就举例了与 
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/cicd.md#%E4%B8%8E-github-action-%E7%9A%84%E9%9B%86%E6%88%90"
              target="blank"
              >Github Action 的集成</a
            >
            、与 
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/cicd.md#%E4%B8%8E-gitee-go-%E7%9A%84%E9%9B%86%E6%88%90"
              target="blank"
              >Gitee Go 的集成</a
            >
            与
            <a
              href="https://github.com/Serverless-Devs/Serverless-Devs/blob/master/docs/zh/cicd.md#%E4%B8%8E-jenkins-%E7%9A%84%E9%9B%86%E6%88%90"
              target="blank"
              >Jenkins 的集成</a
            >
             等平台集成的案例
          </p>
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<style>
.home-feature a {
  text-decoration: underline;
  color: #1b58f4;
}
</style>
