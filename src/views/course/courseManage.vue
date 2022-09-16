<template>
  <v-app>
    <v-card
        color="grey lighten-4"
        flat
        tile
    >
      <v-toolbar dense>
        <v-app-bar-nav-icon></v-app-bar-nav-icon>

        <v-toolbar-title>课程管理</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-heart</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </v-toolbar>
    </v-card>

    <v-container>
      <v-card class="mx-auto mt-6" max-width="90%">
        <v-container class="text-left" v-if="!$vuetify.breakpoint.mobile">
          <v-form ref="form" class="mb-n6" lazy-validation @keyup.enter.native="select">
            <v-text-field
                color="success"
                class="search-textarea mr-3"
                v-model="filter.id"
                append-icon="mdi-magnify"
                label="课程号"
                outlined
                clearable
                dense
            ></v-text-field>
            <v-text-field
                color="success"
                class="search-textarea mr-3"
                v-model="filter.name"
                append-icon="mdi-magnify"
                label="课程名"
                outlined
                clearable
                dense
            ></v-text-field>
            <v-text-field
                color="success"
                class="search-textarea mr-3"
                v-model="filter.teacher"
                append-icon="mdi-magnify"
                label="授课老师"
                outlined
                clearable
                dense
            ></v-text-field>
            <v-text-field
                color="success"
                item-color="success"
                class="search-textarea mr-3"
                append-icon="mdi-magnify"
                v-model="filter.classroom"
                label="教室"
                outlined
                clearable
                dense
            ></v-text-field>
            <v-btn color="success" @click="select" class="mb-1 mr-3" height="40px">筛选</v-btn>
            <v-btn color="warning" @click="clear" class="mb-1" height="40px">清除筛选</v-btn>
          </v-form>
        </v-container>
        <v-divider></v-divider>
        <v-data-table
            :headers="headers"
            :items="filter.courses"
            sitem-key="name"
            :page.sync="page"
            :items-per-page="itemsPerPage"
            hide-default-footer
            disable-sort
            calculate-widths
        >
          <template v-slot:[`item.action`]="{ item }">
            <v-btn text color="primary" class="ml-n3" @click="detail(item)">
              <v-icon small class="mr-2">mdi-pencil</v-icon>查看详情
            </v-btn>
          </template>
        </v-data-table>
        <v-divider></v-divider>
        <v-toolbar flat class="mb-6">
          <v-spacer></v-spacer>
          <v-pagination color="success" v-model="page" :length="pageCount" total-visible="7"></v-pagination>
          <v-toolbar-items v-if="!$vuetify.breakpoint.mobile" class="ml-2 mt-10">
            <span>跳至</span>
            <v-text-field
                color="success"
                v-model="jumpPage"
                style="width: 28px; margin-top: -2px"
                @blur="jump"
                @keyup.enter.native="jump"
                dense
            ></v-text-field>
            <span>页，每页显示</span>
            <v-select
                color="success"
                item-color="success"
                v-model="itemsPerPage"
                :items="itemsPerPageList"
                style="width: 50px; margin-top: -2px"
                dense
            ></v-select>
            <span>条</span>
          </v-toolbar-items>
        </v-toolbar>

      </v-card>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      name: 'courseManage',
      filter: {
        id: '',
        course_id:'',
        name: '',
        teacher: '',
        classroom: '',
        max_capacity: '',
        cur_capacity: '',
        courses: [
          {
            "id": 1,
            "course_id":"1",
            "name": '数据库',
            "teacher": 'Mrs.Lang',
            "classroom": 'F',
            "max_capacity": '100',
            "cur_capacity": '99',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },          {
            "id": 2,
            "course_id":"2",
            "name": '编译技术',
            "teacher": 'Mr.Hu',
            "classroom": 'H',
            "max_capacity": '120',
            "cur_capacity": '119',
          },
        ]
      },
      page: 1,
      jumpPage: '',
      pageCount: 1,
      itemsPerPage: 15,
      itemsPerPageList: [5, 10, 15, 20, 30, 50],
    }
  },
  watch: {
    page: async function () {
      await this.refresh();
    },
    itemsPerPage: async function () {
      await this.updateWithFix();
    }
  },
  methods: {
    async refresh() {
      this.pageCount = Math.ceil(this.filter.courses.length / this.itemsPerPage);
      console.log(this.pageCount);
    },
    async jump() {
      let next = !isNaN(parseInt(this.jumpPage, 10)) ? parseInt(this.jumpPage) : this.page;
      next = Math.min(Math.max(1, next), this.pageCount);
      if (next !== this.page) {
        this.page = next;
      }
      this.jumpPage = '';
    },
    async select() {
      await this.updateWithFix();
    },
    async updateWithFix() {
      if (this.page === 1) {
        await this.refresh();
      } else {
        this.page = 1;
      }
    },
    hasSelect() {
      if (this.filter.id !== null && this.filter.id !== '') {
        return true;
      }
      if (this.filter.name !== null && this.filter.name !== '') {
        return true;
      }
      return this.filter.role !== null && this.filter.role !== '';
    },
    async clear() {
      if (this.hasSelect()) {
        this.$refs.form.reset();
        await this.updateWithFix();
      }
    },
    detail(item) {
      this.$router.push({
        path: 'course-info/' + item['id'],
        query: {
          id: item['id'],
          course_id: item['course_id'],
          name: item['name'],
          teacher: item['teacher'],
          classroom: item['classroom'],
          max_capacity: item['max_capacity'],
          cur_capacity: item['cur_capacity'],
        }
      });
    },
  },
  computed: {
    headers() {
      return [
        {
          text: 'ID',
          value: 'id'
        },
        {
          text: '课程号',
          value: 'course_id'
        },
        {
          text: '课程名',
          value: 'name'
        },
        {
          text: '授课老师',
          value: 'teacher'
        },
        {
          text: '教室',
          value: 'classroom',
          width: '12%'
        },
        {
          text: '最大容量',
          value: 'max_capacity'
        },
        {
          text: '当前容量',
          value: 'cur_capacity'
        },
        {
          text: '课程管理',
          value: 'action',
          width: '32%'
        }
      ];
    }
  }
}
</script>

<style scoped>
.search-textarea {
  display: inline-block;
  width: 15%;
}
</style>