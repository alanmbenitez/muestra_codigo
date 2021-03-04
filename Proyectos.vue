<template>
    <section class="schools__project__main">
        <article>
            <h2 class="schools__project__text text-raj">{{ texto }}</h2>
        </article>
        <client-only>
            <VueSlickCarousel
                v-if="proyectos.length > 0"
                ref="carousel"
                class="schools__project__carousel"
                v-bind="carousel_settings"
            >
                <a
                    v-for="(card, index) in proyectos"
                    :key="index"
                    class="schools__project__carousel__link"
                    :title="card.title"
                    target="_blank"
                    :href="card.href"
                >
                    <LazyImage
                        :source="card.imagen"
                        :alt="`Imagen de proyecto`"
                        class="schools__project__carousel__img"
                    />
                </a>

                <template #customPaging="page">
                    <div class="schools__project__carousel__page custom-dot">{{ page }}</div>
                </template>
            </VueSlickCarousel>
        </client-only>
    </section>
</template>
<script>
    import VueSlickCarousel from 'vue-slick-carousel';
    export default {
        components: {
            VueSlickCarousel,
        },
        props: {
            texto: {
                type: String,
                default: 'text',
            },
            proyectos: {
                type: [Object, Array],
                default() {
                    return {};
                },
            },
        },
        data() {
            return {
                carousel_settings: {
                    centerMode: true,
                    centerPadding: '10px',
                    dots: true,
                    arrows: false,
                    lazyLoad: 'ondemand',
                    cssEase: 'ease-in-out',
                    autoplay: true,
                    infinite: true,
                    swipeToSlide: true,
                    dotsClass: 'dots-parent',
                    slidesToShow: 300,
                    responsive: [
                        {
                            breakpoint: 20000,
                            settings: 'unslick',
                        },
                        {
                            breakpoint: 959,
                            settings: {
                                slidesToShow: 2,
                            },
                        },
                        {
                            breakpoint: 639,
                            settings: {
                                slidesToShow: 1,
                                slidesToScroll: 1,
                            },
                        },
                    ],
                },
            };
        },
    };
</script>
<style scoped>
    .schools__project__main {
        @apply relative w-full py-12 bg-dh-gray;
    }
    .schools__project__text {
        @apply text-3xl text-center font-bold text-dh-black pb-4;
    }
    .schools__project__carousel {
        @apply mx-auto w-full flex flex-row justify-center flex-wrap items-center mb-6;
    }
    .schools__project__carousel__link {
        @apply w-19rem h-video block text-center m-6 shadow inline-block relative;
    }
    .schools__project__carousel__link:hover {
        @apply shadow-lg;
    }
    .schools__project__carousel__img {
        @apply w-19rem h-video;
    }
    @media (min-width: 1024px) {
        .schools__project__carousel__page {
            @apply hidden;
        }
    }
</style>
