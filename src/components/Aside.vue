<template>

   

    <el-menu default-active="1" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" :collapse="isCollapse"
    background-color="#545c64"
    text-color="#fff"
    active-text-color="#ffd04b"
    >

        <h3>维C数据采集系统</h3>

        <el-menu-item v-for="item in menus" :index="item.path" :key="item.path"
            @click="clickMenu(item)"
        >
            <i :class="`${item.icon}`"></i>
            <span slot="title">{{ item.name }}</span>
        </el-menu-item>

        <!-- <el-menu-item index="2">
            <i class="el-icon-s-help"></i>
            <span slot="title">公众号列表</span>
        </el-menu-item>
        

        <el-submenu index="3">
            <template slot="title">
                <i class="el-icon-location"></i>
                <span slot="title">其他</span>
            </template>
            <el-menu-item index="1-1">选项1</el-menu-item>
            <el-menu-item index="1-2">选项2</el-menu-item>
        </el-submenu> -->
        
    </el-menu>
</template>
  

<script>
export default {
    data() {
    return {
        isCollapse: false,
        menus: [
            {
                'path': '/',
                'name': '首页',
                'icon': 'el-icon-menu'
            },
            {
                'path': '/wechat',
                'name': '公众号列表',
                'icon': 'el-icon-camera'
            },
            {
                'path': '/user',
                'name': '个人中心',
                'icon': 'el-icon-user-solid'
            }
        ]
    };
    },
    methods: {
        handleOpen(key, keyPath) {
            console.log(key, keyPath);
        },
        handleClose(key, keyPath) {
            console.log(key, keyPath);
        },
        clickMenu(e){

            if (this.$route.path !== e.path && !(this.$route.path =='/home' && e.path ==='/')){
                this.$router.push(e.path);
            }
        }
    }
}
</script>

<style lang="less" scoped>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}

.el-menu {
    height: 100vh;
    h3 {
        font-size: 16px;
        color: #fff;
        text-align: center;
    }
}



.el-aside::-webkit-scrollbar {

display: none;

}

</style>