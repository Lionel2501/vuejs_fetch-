<template>
    <button 
        @click="$emit('toggleForm')" 
        :style="{background:color}" 
        class="btn">
            {{ text }}
    </button>
</template>

<script>
export default {
    name:'Buttons',
    props:{
        text:String,
        color:String
    }
}
</script>