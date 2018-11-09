<template>
        <select id="custom_select" class="select2" :class="extra_classes">
            <option value="0" disabled selected>{{default_option}}</option>
            <option v-for="item in options" :value="item.id" :key="item.id">{{item.text}}</option>
        </select>
</template>

<script>
    export default {
        props: ['options', 'value', 'extra_classes','default_option'],
        mounted: function () {
            var vm = this
            $(this.$el)
            .select2()
            .val(0)
            .on('change', function () {
                vm.$emit('input', this.value)
            })
        },
        watch: {
            value: function (value) {
                // update value
                $(this.$el)
                    .val(value)
                    .trigger('change')
            },
            options: function (options) {
                // update options
                $(this.$el).empty().select2({ data: options })
            }
        },
        destroyed: function () {
            $(this.$el).off().select2('destroy')
        }
    }
</script>
