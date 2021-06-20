<template>
    
    <div>
        <button @click="$emit('nightmode')" class="butt"><img :src="(mode === 'dark') ? moon : sun" alt=""></button>
    </div>

</template>

<script>
import sun from '../assets/images/icon-sun.svg'
import moon from '../assets/images/icon-moon.svg'
export default {
    name: 'Theme',
    props: [
        'mode'
    ],
    
    data() {
        return {
            sun,
            moon,
        }
    }

}
</script>

<style>

</style>