<template>
    <CustomMask :show="isShowPage">
        <main>
            <div class="schools__main_container">
                <!-- ------------------------------Hero---------------------------------- -->
                <Hero
                    :title="$t('colegios.title')"
                    :detail="$t('colegios.detail_hero')"
                    :image-u-r-l="$t('colegios.img_hero')"
                    :is-course="false"
                    :one-button="true"
                    :boton="$t('colegios.boton_hero')"
                />
                <!-- ------------------------- texto  ---------------------------------- -->
                <Texto :texto="$t('colegios.text_pre')" />

                <!-- ------------------------- avalado por ---------------------------------- -->
                <Aval :texto="$t('colegios.cert')" :href="$t('colegios.pdf_cert')" :src="$t('colegios.logo_cert')" />

                <!-- -------------------------- video  ------------------------------------->
                <VideoIntro
                    :url="'tqQGe7xdb0E'"
                    :comment="'Juana, 11 años. Florida Day School'"
                    :detail="titulo_video"
                />

                <!-- ------------------- metodologias de enseñanza------------------------ -->
                <WhyCourse
                    :cards="$t('colegios.cuadros')"
                    :title="$t('colegios.titulo_cards')"
                    cardHeight="h-12rem md:h-auto"
                />

                <!-- ---------------------------opiniones directivos ------------------------- -->
                <Opinion
                    :src="$t('colegios.foto_referente')"
                    :nombre_img="$t('colegios.nombre_referente')"
                    :texto="$t('colegios.opinion')"
                    :referente="$t('colegios.referente')"
                />

                <!-- ----------------------------proyecto alumnos ------------------------------- -->
                <Proyectos :proyectos="$t('colegios.proyectos')" :texto="$t('colegios.title_proyectos')" />

                <!-- ------------------------------logos instituciones---------------------------- -->
                <Logos :texto="$t('colegios.titulo_logos')" :logos="$t('colegios.logos')" />

                <!-- ---------------------------- progreso------------------------------------------ -->
                <Timeline :progreso="$t('colegios.progreso')" />

                <!-- ------------------------------FAQs--------------------------------------------- -->
                <FAQs :preguntas="$t('colegios.faqs')" :title="$t('colegios.title_faqs')" />
            </div>
        </main>
    </CustomMask>
</template>
<script>
    import CustomMask from '~/plugins/Mask.vue';

    export default {
        name: 'Colegios',
        scrollToTop: true,
        components: {
            Hero: () => import('~/components/colegios/Hero.vue'),
            VideoIntro: () => import('~/components/cursos/VideoIntro.vue'),
            WhyCourse: () => import('~/components/cursos/WhyCourse.vue'),
            FAQs: () => import('~/components/faq/Faqs.vue'),
            Texto: () => import('~/components/colegios/Text_ctrl.vue'),
            Aval: () => import('~/components/colegios/Aval.vue'),
            Opinion: () => import('~/components/colegios/Opinion.vue'),
            Proyectos: () => import('~/components/colegios/Proyectos.vue'),
            Logos: () => import('~/components/colegios/Logos.vue'),
            Timeline: () => import('~/components/colegios/Timeline'),
            CustomMask,
        },
        data() {
            return {
                isShowPage: false,
                titulo_video:
                    '"Me gustó porque me enseñaron a hacer páginas web, que es algo que siempre quise hacer. Además las clases fueron interesantes y divertidas"',
            };
        },
        created() {
            setTimeout(() => {
                this.isShowPage = true;
            }, 100);
        },
    };
</script>
<style scoped>
    .schools__main_container {
        @apply bg-dh-gray;
    }
</style>
<style>
    .y-video__inner {
        padding-bottom: 59.25% !important;
    }
</style>
