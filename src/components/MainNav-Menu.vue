<template>
    <div class="MainNav-Menu-main" @click.self="ycMenu()">
        <div class="menulist">
            左侧弹出菜单
        </div>
    </div>
</template>

<script>
export default {
    props:['activemenu'],    
    methods:{
        ycMenu:function(){
            this.$parent.ycmenu()
        }
    }
}
</script>

<style scoped>
.MainNav-Menu-main{
    position: fixed;
    top: 0;
    left: -100vw;
    width: 100vw;
    height: 100vh;
    background: transparent;
    z-index: 40;
    transition: left 0.2s;
}
.menulist{
    width: 70vw;
    height: 100vh;
    background: yellowgreen;

}
.showmenu{
    left: 0;
}
</style>