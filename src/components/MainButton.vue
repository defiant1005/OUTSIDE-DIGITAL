<template>
 <div class="container">
    <button class="main__btn" v-on:click="main.isActive=true">Налоговый вычет</button>
    <Popup 
        v-bind:main="main"
    />
 </div>
</template>

<script>
import Popup from "@/components/Popup"
export default {
    data() {
        return {
            main: {
                isActive: false,
                isOpenCheckbox: true
            },
        }
    },
    components: {
        Popup,
    }
}
</script>

<style src='../../public/styles/main.css'></style>


