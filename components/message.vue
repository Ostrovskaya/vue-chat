<template>
    <div class="">
        <div class="system" v-if="name === 'admin'">
            <p class="text-xs-center">{{text}}</p>
            <hr>
        </div>
        <div class="wrap" v-else>
            <div class="mes" :class="{owner}">
                <small><strong>{{name}}</strong></small>
                <p>{{text}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        name: String,
        text: String,
        owner: {
            type: Boolean,
            default: false
        }
    }
}
</script>

<style lang="sass" scoped>
    .system 
        margin-bottom: 1rem
        & p
            margin-bottom: 1rem
    

    .wrap 
        margin-bottom: 1rem
        display: flex
        flex-direction: column
    

    .mes
        padding: 1rem
        width: 60%
        margin: 0 1rem
        box-shadow: 0px 1px 0px 0px rgba(50, 50, 50, 0.3)
        border-radius: 4px
        background: #1976d2
        position: relative
        margin-bottom: 1rem
        & p
            margin-bottom: 0
    

    .owner 
        background: #ffffff
        color: #000000
        align-self: flex-end
    
</style>