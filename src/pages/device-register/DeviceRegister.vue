<template>
    <div class="body">
        <appForm></appForm>
        <appTable></appTable>
    </div>
</template>

<script>
import Form from './components/Form.vue'
import Table from './components/Table.vue'
export default {
    data() {
        return {

        }
    },
    methods: {

    },
    props: [],
    components: {
        appForm: Form,
        appTable: Table
    }
}
</script>
<style>

</style>