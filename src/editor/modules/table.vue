<template>
    <form @submit.prevent="insertTable" class="form">
        <label>
            <div>Rows</div>
            <input type="number" style="width: 60px"  min="2" v-model="rows">
        </label>
        <label>
            <div>Columns</div>
            <input type="number" style="width: 60px"  min="2" v-model="cols">
        </label>

        <button type="submit">Insert</button>
    </form>
</template>

<script>
// import bus from 'src/editor/bus.js';

export default {
    title: "table",
    description: "Insert Table",
    icon: '<svg style="width:18px;height:18px" viewBox="0 0 24 24"><path class="ql-fill" d="M5,4H19A2,2 0 0,1 21,6V18A2,2 0 0,1 19,20H5A2,2 0 0,1 3,18V6A2,2 0 0,1 5,4M5,8V12H11V8H5M13,8V12H19V8H13M5,14V18H11V14H5M13,14V18H19V14H13Z" /></svg>',

    data(){
        return {
            rows: 2,
            cols: 2
        }
    },
    methods: {
        insertTable(){
            const rows = (
              "<tr>" + "<td></td>".repeat(this.cols) + "</tr>"
            ).repeat(this.rows);

            this.$emit("exec", "insertHTML", `<table><tbody>${rows}</tbody></table>`);
            this.$parent.closeDashboard()

        }
    }
};

</script>
<style lang="stylus" scoped>
.form
  display: flex;
  align-content: flex-end;

  label
    margin-right 1rem

</style>
