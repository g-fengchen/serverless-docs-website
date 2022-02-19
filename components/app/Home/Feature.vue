<template>
  <div class="home-feature py-10 px-10">
    <el-row :gutter="60">
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">{{ $t("home.featureLock.name") }}</p>
          <p class="text-sm" v-html='$t("home.featureLock.content")'>
          </p>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">{{ $t("home.featureOpenSource.name") }}</p>
          <p class="text-sm" v-html='$t("home.featureOpenSource.content")' />
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">{{ $t("home.featurePluggable.name") }}</p>
          <p class="text-sm" v-html='$t("home.featurePluggable.content")' />
        </div>
      </el-col>
    </el-row>

    <el-row :gutter="60" class="mt-8">
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">{{ $t("home.featureEasy.name") }}</p>
          <p class="text-sm" v-html='$t("home.featureEasy.content")' />
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">{{ $t("home.featureLifecycle.name") }}</p>
          <p class="text-sm" v-html='$t("home.featureLifecycle.content")' />
        </div>
      </el-col>
      <el-col :span="8">
        <div class="text-center">
          <p class="text-xl font-bold my-4">{{ $t("home.featureIntegration.name") }}</p>
          <p class="text-sm" v-html='$t("home.featureIntegration.content")' />
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
