<template>
        <select id="custom_select" class="select2" :class="extra_classes" data-placeholder="Select an option">
            <option value="0" selected="selected">{{default_option}}</option>
            <option v-for="item in options" :value="item.id" :key="item.id">{{item.text}}</option>
        </select>
</template>

<script>
    export default {
        props: ['options', 'extra_classes','default_option'],
        mounted: function () {
            var vm = this
            $(this.$el)
            .on('change', function () {
                vm.$emit('input', this.value)
            })
        },
        watch: {
            
        },
        destroyed: function () {
            $(this.$el).off().select2('destroy')
        }
    }
</script>
