<template>
    <CustomMask :show="isShowPage">
        <main>
            <div class="bg-dh-gray">
                <!-- ---------------------------HERO------------------ -->
                <Hero :title="$t('empresas.title')" :is-course="false" :one-button="false" />
                <!-- ----------------------- -CONTACTO---------------------------------------------------------- -->

                <Contacto
                    :title="$t('empresas.subtitle')"
                    :email="$t('empresas.email')"
                    :telefono="$t('empresas.tel')"
                />
                <!-- - --------------------------- BANNER    -------------------------- -->

                <Banner
                    :title="$t('empresas.title_txt')"
                    :texto="$t('empresas.texto_parrafo')"
                    :boton="$t('empresas.btn_parrafo')"
                />
                <!--  ---------------------------------- hero programas -------------------------------------- -->
                <Hero :title="$t('empresas.banner_medio')" :is-course="false" :one-button="false" />
                <!-- --------------------------------------PROGRAMAS ------------------------------- -->

                <Programas :programas="$t('empresas.cards')" />

                <!--------------------------------------CARDS---------------------------------- -->
                <WhyCourse :cards="$t('empresas.cuadros')" :title="$t('empresas.title_card')" />
                <!-- ------------------------------------------------------------- -->
                <!-- <VueSlickCarousel
                v-if="empresas.opiniones && empresas.opiniones.length > 0"
                ref="carousel"
                v-bind="carousel_settings"
            > -->
                <Opinion
                    v-for="(opinion, index) in empresas.opiniones"
                    :key="index"
                    :src="opinion.foto_referente"
                    :nombre_img="opinion.nombre_referente"
                    :texto="opinion.opinion"
                    :referente="opinion.referente"
                />
                <!--       <template #customPaging="page">
                    <div class="custom-dot lg:hidden">
                        {{ page }}
                    </div>
                </template>
            </VueSlickCarousel> -->
                <!-- ---------------------------------   LOGOS------------------------------------- -->
                <Logos :texto="$t('empresas.titulo_logos')" :logos="$t('empresas.logos')" :color="color" />
                <!-- ------------------------Videos -------------------------------- -->
                <Videos :all-videos="empresas.videos" />
            </div>
        </main>
    </CustomMask>
</template>

<script>
    import { mapState } from 'vuex';
    import CustomMask from '~/plugins/Mask.vue';
    import deadpool from '@/mixins/deadpool';

    export default {
        name: 'Empresas',
        scrollToTop: true,
        components: {
            Hero: () => import('~/components/general/HeroGral.vue'),
            Opinion: () => import('~/components/colegios/Opinion.vue'),
            WhyCourse: () => import('~/components/cursos/WhyCourse.vue'),
            Logos: () => import('~/components/colegios/Logos.vue'),
            Programas: () => import('~/components/empresas/Programas.vue'),
            Contacto: () => import('~/components/empresas/BannerContacto.vue'),
            Banner: () => import('~/components/empresas/Banner.vue'),
            Videos: () => import('~/components/empresas/Videos.vue'),
            CustomMask,
        },
        mixins: [deadpool],
        data() {
            return {
                isShowPage: false,
                color: 'bg-dh-gray',
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
                metas: {
                    title: `${this.$t('business.meta.title')} || Digital House`,
                    description: this.$t('business.meta.description'),
                    src: '',
                },
            };
        },
        computed: {
            ...mapState({
                empresas: (state) => state.empresas,
            }),
        },
        created() {
            setTimeout(() => {
                this.isShowPage = true;
            }, 100);
        },
        head() {
            return {
                title: this.metas.title,
                meta: this.metaMetas(this.metas),
                link: [
                    {
                        rel: 'canonical',
                        href: `https://www.digitalhouse.com/${this.$env('APP_COUNTRY')}/${this.$t('routes.business')}`,
                    },
                    {
                        rel: 'alternate',
                        href: `https://www.digitalhouse.com/latam/${this.$t('routes.business', 'es-AR')}`,
                        hreflang: 'es',
                    },
                    {
                        rel: 'alternate',
                        href: `https://www.digitalhouse.com/ar/${this.$t('routes.business', 'es-AR')}`,
                        hreflang: 'es-AR',
                    },
                    {
                        rel: 'alternate',
                        href: `https://www.digitalhouse.com/br/${this.$t('routes.business', 'pt-BR')}`,
                        hreflang: 'pt-BR',
                    },
                    {
                        rel: 'alternate',
                        href: `https://www.digitalhouse.com/mx/${this.$t('routes.business', 'es-MX')}`,
                        hreflang: 'es-MX',
                    },
                    {
                        rel: 'alternate',
                        href: `https://www.digitalhouse.com/${this.$t('routes.business', 'es-AR')}`,
                        hreflang: 'x-default',
                    },
                ],
            };
        },
    };
</script>

<style>
    .minWidth {
        min-width: 19rem;
    }
    .maxWidth {
        max-width: 32rem;
    }
</style>
