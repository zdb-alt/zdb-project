<template>
  <div>
      <!-- 可查看完整路由信息 -->
      <!-- <pre>{{ route }}</pre> -->
    <div class="column-detail-page w-75 mx-auto">
      <div class="column-info row mb-4 border-bottom pb-4 align-items-center" v-if="column">
        <div class="col-3 text-center">
          <img :src="column.avatar && column.avatar.fitUrl" :alt="column.title" class="rounded-circle border w-100">
        </div>
        <div class="col-9">
          <h4>{{column.title}}</h4>
          <p class="text-muted">{{column.description}}</p>
        </div>
      </div>
      <post-list :list="list"></post-list>
    </div>
  </div>
</template>

<script lang="ts">
import { useStore } from 'vuex'
import { GlobalDataProps } from '../store'
import PostList from '../components/PostList.vue'
import { computed, defineComponent } from 'vue'
import {  useRoute } from 'vue-router'
export default defineComponent({
  components:{
    PostList
  },
  setup(){
    const route=useRoute()
    const store=useStore<GlobalDataProps>()
    const currentId=+route.params.id
    const column = computed(()=> store.getters.getColumnById(currentId) )
    const list= computed(()=> store.getters.getPostsByCid(currentId))
    return{
      column,
      list,
      // route
    }
  }
});
</script>

<style lang="scss" scoped>

</style>
