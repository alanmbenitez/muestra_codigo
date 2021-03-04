<template>
   <main class="schools__logos__main">
        <h2 class="schools__logos__text text-raj">
            {{ texto }}
        </h2>
        <section class="schools__logos__section">
            <article :class="'schools__logos__article' + color">
                <div v-for="(logo, index) in logos" :key="index" class="schools__logos__div">
                    <LazyImage :source="logo.imagen" :alt="`Imagen de logo`" />
                </div>
            </article>
        </section>
    </main>
</template>
<script>
    export default {
        props: {
            texto: {
                type: String,
                default: 'text',
            },
            color: {
                type: String,
                default: ' bg-white',
            },
            logos: {
                type: [Object, Array],
                default() {
                    return {};
                },
            },
        },
    };
</script>
<style scoped>
    .schools__logos__main {
        @apply bg-dh-gray py-8;
    }
    .schools__logos__text {
        @apply text-3xl text-center font-bold text-dh-black pb-4;
    }
    .schools__logos__section {
        @apply w-full mr-auto ml-auto block;
    }
    .schools__logos__article {
        @apply w-full my-0 mx-auto max-w-948px p-4 rounded flex flex-wrap justify-around items-center shadow;
    }
    .schools__logos__div {
        @apply w-1/5 mx-1;
    }
</style>
