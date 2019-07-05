<template>
    <div>
        <button type="button" @click="insertHeading">H1</button>
        <button type="button" @click="insertHeading">H2</button>
        <button type="button" @click="insertHeading">H3</button>
        <button type="button" @click="insertHeading">H4</button>
        <button type="button" @click="insertHeading">H5</button>
        <button type="button" @click="insertHeading">H6</button>
    </div>
</template>

<script>
export default {
    title: "headings",
    description: "Headings (h1-h6)",
    icon: '<svg style="width:18px;height:18px" viewBox="0 0 24 24"><path class="ql-fill" d="M3,12H6V19H9V12H12V9H3M9,4V7H14V19H17V7H22V4H9Z" /></svg>',

    methods: {
        insertHeading(e){
            this.$parent.closeDashboard();
            this.$emit("exec", "formatBlock", e.target.textContent);
        }
    }
};

</script>

