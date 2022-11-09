<template>
    <header class="header bg-gray-900">
        <section class="container mx-auto flex justify-between">
            <TheLogoMenu />
            <TheNavBar />
        </section>
    </header>
</template>
<script >
import TheNavBar from './TheNavBar.vue'
import TheLogoMenu from './TheLogoMenu.vue'
export default{
    components:{
        TheNavBar,
        TheLogoMenu
    }
}
</script>
