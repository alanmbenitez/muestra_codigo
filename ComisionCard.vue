<template>
    <article :class="getArticleStyle" @mouseleave="popShow = false">
        <section class="comision_card__date_box font-mon">
            <div class="comision_card__date__title_div">
                <h3 :class="getCardTitleStyle">{{ formated_date }}</h3>
            </div>
            <div :class="getCardSubTitleDivStyle">
                <h3 :class="getCardSubTitleStyle">{{ days }}</h3>
            </div>
        </section>
        <section class="comision_card__information_section">
            <div class="card__information_section__div">
                <div class="card__information_clock__div">
                    <ClockIcon :class="getClockIconStyle" />
                    <span :class="getDateRangeStyles">{{ dateRange }}</span>
                </div>
                <div v-if="true" class="card__information_cloud__div" @mouseover="popShow = true">
                    <CloudIcon :class="getCloudIconStyle" />
                    <span :class="getModalityTextStyle">{{ $t('cursos.modality_remote') }}</span>
                </div>
                <div v-else class="card__information_location_div">
                    <LocationIcon class="h-5 w-5 mr-1" />
                    <span class="card__information__text">Sede</span>
                </div>
            </div>
            <div class="comision--discount_box">
                <span :class="getDiscountSyle">{{ amoutn_of_discount }}</span>
                <button :class="getButtonStyles" :disabled="getDisabledButton">
                    {{ $t(getButtonText) }}
                </button>
            </div>
        </section>
        <aside
            v-if="popShow"
            class="card__information_modalities_div"
            @mouseover="popShow = true"
            @mouseleave="popShow = false"
        >
            {{ $t('cursos.modality_button_info') }}
            <button class="card__information_modalities_btn" @click.self.prevent="openPopLink">
                {{ $t('cursos.modality_title') }}
            </button>
        </aside>
    </article>
</template>
<script>
    export default {
        components: {
            ClockIcon: () => import('~/components/icons/ClockIcon'),
            CloudIcon: () => import('~/components/icons/CloudIcon'),
            LocationIcon: () => import('~/components/icons/LocationIcon'),
        },
        props: {
            available: {
                type: Number,
                default: 1,
            },
            created_at: {
                type: String,
                default: '2020-05-20T13:05:12.000Z',
            },
            dateRange: {
                type: String,
                default: '08:30 a 12:00 hs',
            },
            days: {
                type: String,
                default: 'lunes, martes, miércoles',
            },
            discount: {
                type: Number,
                default: 0,
            },
            discountMat: {
                type: Number,
                default: 0,
            },
            endDate: {
                type: String,
                default: '01-10-2020T00:00:00',
            },
            id: {
                type: Number,
                default: 1,
            },
            matMessage: {
                type: String,
                default: 'mensaje de matrícula dfd',
            },
            message: {
                type: String,
                default: 'Test messagefdf ',
            },
            price: {
                type: Number,
                default: 0,
            },
            priceMat: {
                type: Number,
                default: 0,
            },
            priceMessage: {
                type: String,
                default: 'mensaje de cuotas fd f',
            },
            sede: {
                type: Object,
                default() {
                    return {};
                },
            },
            sede_id: {
                type: Number,
                default: 1,
            },
            startDate: {
                type: String,
                default: '20-05-2020T00:00:00',
            },
            turn: {
                type: String,
                default: 'mañana',
            },
            updated_at: {
                type: String,
                default: '2020-05-20T10:05:18.000Z',
            },
            virtualCourse: {
                type: Number,
                default: 1,
            },
        },
        data() {
            return {
                popShow: false,
                months: this.$t('cursos.modal'),
            };
        },
        computed: {
            formated_date() {
                return (this.parseStartDate() + ' - ' + this.parseEndDate()).replace(/\./g, '');
            },
            amoutn_of_discount() {
                return this.discount ? this.discount + '% OFF' : null;
            },
            getCardTitleStyle() {
                const titleStyle = 'comision_card__date__title font-raj ';
                return this.available === 0
                    ? titleStyle + 'crossed_text text-dh-red opacity-50'
                    : titleStyle + 'text-dh-red';
            },
            getButtonText() {
                return this.available === 0
                    ? 'cursos.sold_out'
                    : this.available === 2
                    ? 'cursos.last_quotas'
                    : 'cursos.apply_short';
            },
            getButtonStyles() {
                return this.available === 0 ? 'comision--btn__disabled' : 'comision--btn';
            },
            getDisabledButton() {
                return this.available === 0;
            },
            getCardSubTitleStyle() {
                const subtitleStyle = 'comision_card__days__text ';
                return this.available === 0 ? subtitleStyle + 'crossed_text' : subtitleStyle;
            },
            getCardSubTitleDivStyle() {
                const divStyle = 'comision_card__days_div ';
                return this.available === 0 ? divStyle + 'bg-gray-500' : divStyle + 'bg-gray-300';
            },
            getClockIconStyle() {
                const iconStyle = 'card__information_clock__div__icon ';
                return this.available === 0 ? iconStyle + 'text-gray-700' : iconStyle;
            },
            getDateRangeStyles() {
                const dateRangeStyle = 'card__information_clock__div__text ';
                return this.available === 0 ? dateRangeStyle + 'crossed_text text-gray-700' : dateRangeStyle;
            },
            getCloudIconStyle() {
                const iconStyle = 'cloud_icon ';
                return this.available === 0 ? iconStyle + 'text-gray-700' : iconStyle;
            },
            getModalityTextStyle() {
                const modalityStyle = 'card__information__text ';
                return this.available === 0 ? modalityStyle + 'crossed_text text-gray-700' : modalityStyle;
            },
            getDiscountSyle() {
                const discountSyle = 'card__information_discount_text font-raj ';
                return this.available === 0
                    ? discountSyle + 'crossed_text text-dh-red opacity-50'
                    : discountSyle + 'text-dh-red';
            },
            getArticleStyle() {
                const articleStyle = 'comision_card ';
                return this.available === 0
                    ? articleStyle + 'cursor-not-allowed bg-gray-300'
                    : articleStyle + 'cursor-pointer bg-white';
            },
        },
        methods: {
            openPopLink() {
                window.open(this.$t('route.modalidad_remote'));
            },
            parseDate(date_string) {
                return this.$moment(date_string).tz(this.$env('APP_TIMEZONE'));
            },
            parseStartDate() {
                const date_object = this.parseDate(this.startDate);
                return `${date_object.date()} ${this.months[date_object.month()]}`;
            },
            parseEndDate() {
                const date_object = this.parseDate(this.endDate);
                return `${date_object.date()} ${this.months[date_object.month()]}`;
            },
        },
    };
</script>
<style scoped>
    .crossed_text {
        text-decoration: line-through;
    }
    .comision_card {
        max-width: 800px;
        @apply w-full rounded relative my-5 overflow-hidden shadow leading-none;
    }
    .comision--discount_box {
        @apply w-full order-2 flex-col  text-center font-bold mt-3;
    }
    .comision--btn {
        @apply uppercase mt-4 rounded py-2 font-bold text-center w-full text-white  bg-dh-red transition duration-300 ease-in-out;
    }
    .comision--btn__disabled {
        @apply uppercase cursor-not-allowed mt-4 rounded py-2 font-bold text-center text-white w-full bg-gray-500;
    }
    .comision--btn:hover {
        @apply bg-white text-dh-red shadow-dh-btn;
    }
    .cloud_icon {
        height: 24px;
        width: 24px;
        @apply mr-1 text-xl;
    }
    .comision_card__date_box {
        @apply w-full text-center font-bold;
    }
    .comision_card__date__title_div {
        @apply text-dh-red uppercase bg-transparent px-1 pt-3 pb-2 rounded-t;
    }
    .comision_card__date__title {
        @apply text-left pl-4 text-2xl;
    }
    .comision_card__days_div {
        @apply text-dh-red uppercase py-2 px-5 text-gray-800 text-left;
    }
    .comision_card__days__text {
        @apply text-sm;
    }
    .comision_card__information_section {
        @apply p-4 flex flex-col font-osa justify-between;
    }
    .card__information_section__div {
        @apply order-1 flex flex-col justify-between items-start;
    }
    .card__information_clock__div {
        height: 50%;
        @apply text-lg flex items-center mb-4;
    }
    .card__information_clock__div__icon {
        @apply h-6 w-6 mr-1 ml-1 text-xl;
    }
    .card__information_clock__div__text {
        width: 80%;
        @apply ml-3;
    }
    .card__information_cloud__div {
        height: 50%;
        @apply text-left text-2xl p-1 flex items-center;
        cursor: default;
    }
    .card__information__text {
        @apply font-bold ml-3;
    }
    .card__information__text:hover {
        @apply text-dh-red;
    }
    .card__information_location_div {
        height: 50%;
        @apply text-lg flex items-center;
    }
    .card__information_discount_text {
        @apply w-full ml-auto mr-0 text-base justify-center items-center h-12 text-3xl;
    }
    .card__information_modalities_div {
        @apply absolute text-left rounded bg-white shadow-xl px-4 py-4 top-0 mt-24 mx-auto leading-normal text-sm;
    }
    .card__information_modalities_btn {
        @apply font-bold underline text-dh-red;
    }
    .card__information_modalities_btn:hover {
        @apply text-dh-red-200;
    }
    @media (min-width: 768px) {
        .comision_card__date__title {
            @apply text-3xl pl-5;
        }
        .comision_card__days_div {
            @apply text-left px-6;
        }
        .comision_card__days__text {
            @apply text-base;
        }
        .comision_card__information_section {
            @apply px-6 flex-row;
        }
        .card__information_section__div {
            @apply text-lg;
        }
        .card__information_clock__div {
            @apply text-xl mb-0;
        }
        .card__information_clock__div__text {
            width: 80%;
            @apply px-2;
        }
        .card__information__text {
            @apply px-2;
        }
        .card__information_location_div {
            @apply text-2xl;
        }
        .card__information_discount_text {
            @apply text-center flex pl-0;
        }
        .comision--discount_box {
            @apply text-center;
        }

        .comision--btn,
        .comision--btn__disabled {
            width: 220px;
        }
    }
    @media screen and (min-width: 768px) {
        .comision--btn,
        .comision--btn__disabled {
            width: 230px;
            @apply mt-0 py-3 text-2xl ml-auto mr-0 block;
        }
        .comision_card {
            min-width: 300px;
            height: 215px;
            @apply mx-auto w-full mb-10;
        }
        .comision--discount_box {
            width: 224px;
            @apply mt-0 pl-1;
        }
    }
    @media (min-width: 1300px) {
        .card__information_clock__div__text {
            width: 80%;
        }
    }
</style>
