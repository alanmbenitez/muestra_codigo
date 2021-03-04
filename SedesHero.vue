<template>
    <client-only>
        <VueSlickCarousel
            v-if="getCampusImages && getCampusImages.length > 0"
            ref="carousel"
            v-bind="carousel_settings"
            class="carousel-true-height"
        >
            <picture v-for="(image, index) in getCampusImages" :key="index" class="main_images_banner__body">
                <img class="images_banner_container__item" :src="image.url" :alt="'Imagen de ' + image.url" />
            </picture>
            <template #customPaging="page">
                <div class="custom-dot">
                    {{ page }}
                </div>
            </template>
        </VueSlickCarousel>
    </client-only>
</template>

<script>
    export default {
        props: {
            getCampusImages: {
                type: Array,
                default: () => [],
            },
        },
        data() {
            return {
                isShowPages: false,
                carousel_settings: {
                    centerMode: true,
                    dots: true,
                    arrows: false,
                    lazyLoad: 'ondemand',
                    cssEase: 'ease-in-out',
                    autoplay: true,
                    infinite: true,
                    swipeToSlide: true,
                    dotsClass: 'dots-parent',
                    slidesToShow: 30,
                    responsive: [
                        {
                            breakpoint: 20000,
                            settings: 'unslick',
                        },
                        {
                            breakpoint: 1023,
                            settings: {
                                slidesToShow: 3,
                            },
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
                metas: {
                    title: `${this.active.sede} || Digital House`,
                    description: this.active.description || '',
                    src: '',
                },
            };
        },
    };
</script>
