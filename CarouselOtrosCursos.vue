<template>
    <section v-if="others.length > 0" class="others">
        <h2 class="others--title font-raj">{{ $t('cursos.other_courses') }}</h2>
        <client-only>
            <VueSlickCarousel v-if="others.length > 0" ref="carousel" class="others--boxes" v-bind="carousel_settings">
                <OtroCurso
                    v-for="(other, index) in others"
                    :key="index"
                    :title="other.title"
                    :slug="other.slug"
                    :detail="other.detail"
                />
                <template #customPaging="page">
                    <div class="custom-dot lg:hidden">
                        {{ page }}
                    </div>
                </template>
            </VueSlickCarousel>
        </client-only>
        <nuxt-link :to="'/cursos'" class="others--link">
            {{ $t('home.see_more') }}
        </nuxt-link>
    </section>
</template>
<script>
    import { mapGetters, mapState } from 'vuex';
    import VueSlickCarousel from 'vue-slick-carousel';
    import '~/node_modules/vue-slick-carousel/dist/vue-slick-carousel.css';
    import OtroCurso from '~/components/cursos/OtroCurso';

    export default {
        components: {
            OtroCurso,
            VueSlickCarousel,
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
                    autoplay: false,
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
                            breakpoint: 1023,
                            settings: {
                                slidesToShow: 3,
                            },
                        },
                        {
                            breakpoint: 930,
                            settings: {
                                slidesToShow: 2,
                            },
                        },
                        {
                            breakpoint: 620,
                            settings: {
                                slidesToShow: 1,
                                slidesToScroll: 1,
                            },
                        },
                    ],
                },
            };
        },
        computed: {
            ...mapState({
                curso: (state) => state.curso.active,
            }),
            ...mapGetters({
                filtrados: 'curso/getFiltered',
            }),
            others() {
                const proxy = [];
                for (let i = 0; i < this.filtrados.length; i++) {
                    const curso = this.filtrados[i];
                    // console.log('curso ' + curso.title);
                    // console.log('actual ' + this.curso.title);
                    if (curso.title !== this.curso.title) {
                        proxy.push(curso);
                        // console.log('agrego ' + curso.title);
                    }
                }
                // console.log('lista ', proxy);
                return proxy;
            },
        },
    };
</script>
<style scoped>
    .others {
        @apply bg-dh-gray mx-auto w-full pt-4 pb-8;
    }
    .others--title {
        @apply mb-4 text-dh-black font-bold text-4xl text-center;
    }
    .others--boxes {
        max-width: 948px;
        @apply mb-8 w-full mx-auto;
    }
    .others--link {
        @apply mt-5 mx-auto my-4 py-2 px-4 rounded transition duration-300 bg-dh-red text-white font-bold block w-40 text-center;
    }
    .others--link:hover {
        @apply shadow-dh-btn;
    }
    @media screen and (min-width: 1024px) {
        .others--boxes {
            @apply flex justify-center;
        }
    }
</style>
