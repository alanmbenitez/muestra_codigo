<template>
    <section class="schools__main">
        <article>
            <p class="schools__text">
                {{ texto }}
            </p>
            <a title="Ministerio de Educacion" target="_blank" :href="href">
                <LazyImage
                    :source="src"
                    :alt="`Imagen de logo`"
                    class="schools__logo transition-3 hover:shadow-btn-dh"
                />
            </a>
        </article>
    </section>
</template>
<script>
    export default {
        props: {
            texto: {
                type: String,
                default: 'text',
            },
            href: {
                type: String,
                default: 'text',
            },
            src: {
                type: String,
                default: 'text',
            },
        },
    };
</script>
<style scoped>
    .schools__main {
        @apply bg-dh-gray w-full mx-auto pb-12 text-center;
    }
    .schools__text {
        @apply w-11/12 max-w-screen-sm text-center mx-auto text-lg leading-normal pt-4;
    }
    .schools__logo {
        @apply max-w-xs bg-white mx-auto shadow my-4 p-4 rounded;
    }
</style>
