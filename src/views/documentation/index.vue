<template>
  <div class="app-container documentation-container">
<!--    <a class="document-btn" target="_blank"
       href="https://store.akveo.com/products/vue-java-admin-dashboard-spring?utm_campaign=akveo_store-Vue-Vue_demo%2Fgithub&utm_source=vue_admin&utm_medium=referral&utm_content=demo_English_button"
    >Java backend integration</a>
    <a class="document-btn" target="_blank" href="https://panjiachen.github.io/vue-element-admin-site/"
    >Documentation</a>
    <a class="document-btn" target="_blank" href="https://github.com/PanJiaChen/vue-element-admin/">Github
      Repository</a>
    <a class="document-btn" target="_blank" href="https://panjiachen.gitee.io/vue-element-admin-site/zh/">国内文档</a>
    <dropdown-menu class="document-btn" :items="articleList" title="系列文章"/>
    <a class="document-btn" target="_blank" href="https://panjiachen.github.io/vue-element-admin-site/zh/job/">内推招聘</a>-->
    <div class="block">
      <el-cascader
        id="roleCas"
        v-model="casValue"
        :options="options"
        clearable
        @change="casChange"
        :props="props"
      ></el-cascader>
    </div>
    <div>
      <a-select v-model="select" style="width: 200px" @change="selectChange">
        <a-select-option value="jack">Jack</a-select-option>
        <a-select-option value="lucy">Lucy</a-select-option>
      </a-select>
    </div>
  </div>
</template>

<script>
import DropdownMenu from '@/components/Share/DropdownMenu'

export default {
  name: 'Documentation',
  components: { DropdownMenu },
  data() {
    return {
      articleList: [
        { title: '基础篇', href: 'https://juejin.im/post/59097cd7a22b9d0065fb61d2' },
        { title: '登录权限篇', href: 'https://juejin.im/post/591aa14f570c35006961acac' },
        { title: '实战篇', href: 'https://juejin.im/post/593121aa0ce4630057f70d35' },
        { title: 'vue-admin-template 篇', href: 'https://juejin.im/post/595b4d776fb9a06bbe7dba56' },
        { title: 'v4.0 篇', href: 'https://juejin.im/post/5c92ff94f265da6128275a85' },
        { title: '自行封装 component', href: 'https://segmentfault.com/a/1190000009090836' },
        { title: '优雅的使用 icon', href: 'https://juejin.im/post/59bb864b5188257e7a427c09' },
        { title: 'webpack4（上）', href: 'https://juejin.im/post/59bb864b5188257e7a427c09' },
        { title: 'webpack4（下）', href: 'https://juejin.im/post/5b5d6d6f6fb9a04fea58aabc' }
      ],
      casValue: [],
      props: {
        multiple: true,
        checkStrictly: true,
        emitPath: true,
        disabled: 'disabled'
      },
      options: [{
        value: 1,
        label: '管理员',
        // disabled: true,
        children: [{
          label: '管理员1级',
          disabled: false,
          value: 11
        }, {
          value: 12,
          disabled: false,
          label: '管理员2级'
        }, {
          value: 13,
          disabled: false,
          label: '管理员3级'
        }]
      }, {
        value: 2,
        label: '学员',
        children: [{
          label: '学员1级',
          value: 21,
          disabled: false
        }, {
          value: 22,
          label: '学员2级',
          disabled: false
        }, {
          value: 23,
          label: '学员3级',
          disabled: false
        }]
      }, {
        value: 3,
        label: '教员',
        children: [{
          label: '教员1级',
          value: 31,
          disabled: false
        }, {
          value: 32,
          label: '教员2级',
          disabled: false
        }, {
          value: 33,
          label: '教员3级',
          disabled: false
        }]
      }]
    }
  },
  mounted() {
  },
  methods: {
    casChange(val) {
      console.log(val)
    },
    selectChange(val){
      console.log(arguments)
    }
  },
  watch: {
    casValue: {
      handler(newVal, oldValue) {
        // 如果清空选择,把所有disabled设置为false
        if (newVal.length === 0) {
          this.options.forEach(item => {
            item.children.forEach(child => {
              child.disabled = false
            })
          })
        } else {
          // 把选中项的其他child设置为disable
          newVal.forEach(item => {
            this.options.forEach(op => {
              if (op.value === item[0]) {
                op.children.forEach(child => {
                  if (child.value !== item[1]) {
                    child.disabled = true
                  }
                })
              }
            })
          })
          // 拿到选中的岗位id
          let select = newVal.map(item => {
            return item[0]
          })
          // 把没有被选中的岗位的child设置为非禁用
          this.options.forEach(item => {
            if (!select.includes(item.value)) {
              item.children.forEach(child => {
                child.disabled = false
              })
            }
          })
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.documentation-container {
  margin: 50px;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;

  .document-btn {
    flex-shrink: 0;
    display: block;
    cursor: pointer;
    background: black;
    color: white;
    height: 60px;
    padding: 0 16px;
    margin: 16px;
    line-height: 60px;
    font-size: 20px;
    text-align: center;
  }
}
</style>
