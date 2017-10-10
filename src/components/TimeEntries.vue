<template>
  <div>
    <router-link
      v-if="$route.path !== '/time-entries/log-time'"
      to="/time-entries/log-time"
      class="btn btn-primary">
      创建
    </router-link>

    <div v-if="$route.path === '/time-entries/log-time'">
      <h3>创建</h3>
    </div>

    <hr>

    <router-view></router-view>

    <div class="time-entries">
      <p v-if="!plans.length"><strong>还没有任何计划</strong></p>

      <div class="list-group">
      <--
        v-for 循环，注意参数顺序为(item,index) in items
      -->
        <a class="list-group-item" v-for="(plan,index) in plans">
          <div class="row">
            <div class="col-sm-2 user-details">

            <--
            `:src`属性，这个是 vue 的属性绑定简写`v-bind`可以缩写为`:`
             比如 a 标签的`href`可以写为`:href`
            并且在 vue 的指令里就一定不要写插值表达式了(`:src={{xx}}`)， vue 自己会去解析
            -->

              <img :src="plan.avatar" class="avatar img-circle img-responsive" />
              <p class="text-center">
                <strong>
                  {{ plan.name }}
                </strong>
              </p>
            </div>

            <div class="col-sm-2 text-center time-block">
              <h3 class="list-group-item-text total-time">
                <i class="glyphicon glyphicon-time"></i>
                {{ plan.totalTime }}
              </h3>
              <p class="label label-primary text-center">
                <i class="glyphicon glyphicon-calendar"></i>
                {{ plan.date }}
              </p>
            </div>

            <div class="col-sm-7 comment-section">
              <p>{{ plan.comment }}</p>
            </div>

            <div class="col-sm-1">
              <button
                class="btn btn-xs btn-danger delete-button"
                @click="deletePlan(index)">
              X
              </button>
            </div>

          </div>
        </a>

      </div>
    </div>
  </div>
</template>
