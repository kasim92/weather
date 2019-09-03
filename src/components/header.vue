<template>
    <nav class="navbar navbar-light bg-light">
        <span class="navbar-brand mb-0 h1 color">Enjaz-Weather°</span>
    </nav>
</template>

<script>
    export default {
        name: "header"
    }
</script>

<style scoped>

    .navbar-brand{
          background: linear-gradient(117deg, #53a5db, #63b0de, #73bae1, #ecdd64);
          background-size: 800% 800%;
          -webkit-animation: AnimationName 10s ease infinite;
          -moz-animation: AnimationName 10s ease infinite;
          animation: AnimationName 20s ease infinite;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        font-weight: bold;
    }
    @-webkit-keyframes AnimationName {
        0%{background-position:87% 0%}
        50%{background-position:14% 100%}
        100%{background-position:87% 0%}
    }
    @-moz-keyframes AnimationName {
        0%{background-position:87% 0%}
        50%{background-position:14% 100%}
        100%{background-position:87% 0%}
    }
    @keyframes AnimationName {
        0%{background-position:87% 0%}
        50%{background-position:14% 100%}
        100%{background-position:87% 0%}
    }

</style>