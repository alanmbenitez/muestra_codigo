<template>
    <a class="event_card" :href="linkURL">
        <section class="event_card-imagebox">
            <LazyImage :source="thumbnail" :alt="title" class="event_card-lazyimage" />
        </section>
        <section class="event_card-textbox">
            <h3 class="event_card-title">
                {{ title }}
            </h3>
            <div class="flex flex-row items-center justify-around w-auto m-w-full">
                <article class="event_card-box py-1">
                    <!-- <span class="event_card-dot" />-->
                    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 48 48">
                        <path d="M0 0h48v48h-48z" fill="none" />
                        <path
                            d="M38 6h-2v-4h-4v4h-16v-4h-4v4h-2c-2.21 0-3.98 1.79-3.98 4l-.02 28c0 2.21 1.79 4 4 4h28c2.21 0 4-1.79 4-4v-28c0-2.21-1.79-4-4-4zm0 32h-28v-22h28v22zm-24-18h10v10h-10z"
                            fill="#cb1e40"
                        />
                    </svg>
                    <h4 class="event_card-text">
                        <p class="text-base text-dh-red font-extrabold -mb-2">{{ formated_date }}</p>
                        <span>{{ day_date }}</span>
                    </h4>
                </article>
                <article class="event_card-box py-1 items-center">
                    <!-- <span class="event_card-dot" /> -->
                    <svg
                        aria-hidden="true"
                        focusable="false"
                        data-prefix="far"
                        data-icon="clock"
                        role="img"
                        xmlns="http://www.w3.org/2000/svg"
                        viewBox="0 0 512 512"
                        class="svg-inline--fa fa-clock fa-w-16 icons__item"
                        height="16"
                        width="16"
                    >
                        <path
                            fill="#cb1e40"
                            d="M256 8C119 8 8 119 8 256s111 248 248 248 248-111 248-248S393 8 256 8zm0 448c-110.5 0-200-89.5-200-200S145.5 56 256 56s200 89.5 200 200-89.5 200-200 200zm61.8-104.4l-84.9-61.7c-3.1-2.3-4.9-5.9-4.9-9.7V116c0-6.6 5.4-12 12-12h32c6.6 0 12 5.4 12 12v141.7l66.8 48.6c5.4 3.9 6.5 11.4 2.6 16.8L334.6 349c-3.9 5.3-11.4 6.5-16.8 2.6z"
                        ></path>
                    </svg>
                    <h4 class="event_card-text">
                        <!-- <div v-for="(hr, index) in datesFormated" :key="index">
                            <span v-if="hr.country !== 'ar'">{{ hr.country.toUpperCase() }} {{ hr.start }}</span>
                        </div> -->

                        <div>
                            <p class="text-base text-dh-red font-extrabold -mb-2">
                                {{ $t('events.shift_night') }}
                            </p>
                            <p class="text-xs mt-1">{{ date[0].start }} - {{ date[0].end }}</p>
                        </div>
                    </h4>
                </article>
                <article class="event_card-box py-1">
                    <!-- <span class="event_card-dot" /> -->
                    <div class="flex flex-col justify-center items-center mb-4">
                        <svg
                            id="Capa_1"
                            version="1.1"
                            xmlns="http://www.w3.org/2000/svg"
                            xmlns:xlink="http://www.w3.org/1999/xlink"
                            class="svg-inline--fa icons__item -mb-1 mt-1"
                            color="#df3456"
                            fill="currentColor"
                            height="18"
                            width="18"
                            viewBox="0 0 425.963 425.963"
                            style="enable-background: new 0 0 425.963 425.963;"
                            xml:space="preserve"
                        >
                            <g>
                                <path
                                    d="M213.285,0h-0.608C139.114,0,79.268,59.826,79.268,133.361c0,48.202,21.952,111.817,65.246,189.081
		c32.098,57.281,64.646,101.152,64.972,101.588c0.906,1.217,2.334,1.934,3.847,1.934c0.043,0,0.087,0,0.13-0.002
		c1.561-0.043,3.002-0.842,3.868-2.143c0.321-0.486,32.637-49.287,64.517-108.976c43.03-80.563,64.848-141.624,64.848-181.482
		C346.693,59.825,286.846,0,213.285,0z M274.865,136.62c0,34.124-27.761,61.884-61.885,61.884
		c-34.123,0-61.884-27.761-61.884-61.884s27.761-61.884,61.884-61.884C247.104,74.736,274.865,102.497,274.865,136.62z"
                                />
                            </g>
                        </svg>
                        <h4 class="event_card-text mt-1 pb-1">
                            <p style="font-size: 14px;" class="text-dh-red font-extrabold">
                                {{ $t('cursos.modality_remote') }}
                            </p>
                        </h4>
                    </div>
                </article>
            </div>
            <button class="event_card-btn">
                {{ linkText }}
            </button>
        </section>
    </a>
</template>
<script>
    import { mapState } from 'vuex';
    export default {
        props: {
            title: {
                type: String,
                default: 'Default',
            },
            thumbnail: {
                type: String,
                default: 'Default',
            },
            linkText: {
                type: String,
                default: 'Default',
            },
            linkURL: {
                type: String,
                default: 'Default',
            },
            date: {
                type: Array,
                default() {
                    return [];
                },
            },
        },

        data() {
            return {
                cardLatam: false,
                popShow: false,
                default_timezone: 'America/Argentina/Buenos_Aires',
                months: ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12'],
                weekdays: ['Domingo', 'Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes', 'Sábado'],
                /**
                 * Recordar agregar el timezone en el nuxt.config.js
                 */
                timezones: {
                    ar: 'America/Argentina/Buenos_Aires',
                    py: 'America/Asuncion',
                    uy: 'America/Montevideo',
                    co: 'America/Bogota',
                    mx: 'America/Mexico_City',
                },
            };
        },

        computed: {
            // ...mapState('home' ,['eventos']),

            ...mapState({
                eventos: (state) => state.home_old.eventos,
                user_country: (state) => state.configs.real_country,
            }),

            formated_date() {
                return this.parseStartDate().replace(/\./g, '');
            },
            day_date() {
                const fecha = this.parseDate(this.date[0].day);
                return this.weekdays[fecha.day()];
            },
            Timeline_entry() {
                const $eventos = this.eventos;

                if ($eventos.length === 1) {
                    return 'timeline--entry1';
                } else {
                    return 'timeline--entry';
                }
            },
        },
        methods: {
            parseDate(date_string) {
                const fmt = 'YYYY-MM-DDTHH:mm:ss';
                const zone = this.default_timezone;
                return this.$moment.tz(date_string, fmt, zone);
            },
            parseStartDate() {
                const date_object = this.parseDate(this.date[0].day);
                return `${date_object.date()}/${this.months[date_object.month()]}`;
            },
            getTimezome(country_code) {
                return this.timezones[country_code] || this.default_timezone || process.env.APP_TIMEZONE;
            },
        },
    };
</script>
<style scoped>
    .event_card {
        width: 300px;
        @apply bg-white m-5 cursor-pointer rounded shadow-md;
    }
    .event_card-imagebox {
        height: 188px;
        border-top-right-radius: 4px;
        border-top-left-radius: 4px;
        @apply bg-blue-400 w-full;
    }
    .event_card-lazyimage {
        @apply object-cover h-full w-full;
    }
    .event_card-textbox {
        @apply px-3 pt-4 pb-5 flex flex-col;
    }
    .event_card-title {
        @apply font-raj text-center text-2xl mb-4 leading-7 font-medium;
    }
    .event_card-box {
        width: 5.5rem;
        height: 5rem;
        @apply bg-dh-gray  flex flex-col justify-center items-center mb-3;
    }
    .event_card-text {
        @apply overflow-hidden text-center text-sm;
    }
    .event_card-dot {
        @apply w-4 h-4 rounded-full inline-block bg-dh-red ml-8 flex-shrink-0;
    }
    .event_card-btn {
        @apply py-2 px-4 rounded transition duration-300 bg-dh-red text-white font-bold block w-full text-center;
    }
    .event_card-btn:hover {
        @apply shadow-dh-btn;
    }

    @media (min-width: 768px) {
        .event_card-title {
            @apply px-2 h-14;
        }
    }
</style>
