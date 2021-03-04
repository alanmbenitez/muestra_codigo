<template>
    <main v-if="teacher">
        <div class="teachers_article">
            <picture class="teacher_box__image">
                <!-- Poner imagen del profe -->
                <LazyImage
                    v-if="teacher.imageURL"
                    :source="`/imgs/profes/${teacher.imageURL}`"
                    :alt="'Imagen de sede' + teacher.name"
                    class="teacher_box__photo"
                />
                <ProfileCircle v-if="!teacher.imageURL" class="teacher_box__icon" />
            </picture>
            <p v-if="showRol" :class="getRolClass">{{ teacher.rol }}</p>
            <p :class="getNameClass">{{ teacher.name }}</p>
        </div>
    </main>
</template>

<script>
    export default {
        components: {
            ProfileCircle: () => import('~/components/icons/profileCircle'),
        },
        props: {
            teacher: {
                type: Object,
                default() {
                    return {};
                },
                required: true,
            },
            showRol: {
                type: Boolean,
                default: false,
                required: false,
            },
            nameColor: {
                type: String,
                default: 'text-dh-black',
                required: false,
            },
            nameSize: {
                type: String,
                default: 'text-sm',
                required: false,
            },
            rolSize: {
                type: String,
                default: 'text-xs',
                required: false,
            },
        },
        computed: {
            getNameClass() {
                return 'teacher_box__name' + ' ' + this.nameColor + ' ' + this.nameSize;
            },
            getRolClass() {
                return 'teacher_box__rol' + ' ' + this.rolSize;
            },
        },
    };
</script>
<style scoped>
    .teachers_article {
        @apply text-center m-auto my-0;
    }
    .teacher_box__image {
        @apply flex justify-center m-auto;
    }
    .teacher_box__photo {
        height: 90px;
        width: 90px;
        border-radius: 50px;
        -webkit-filter: grayscale(100%); /* Safari 6.0 - 9.0 */
        filter: grayscale(100%);
    }
    .teacher_box__icon {
        width: 100px;
        color: rgb(173, 173, 173);
        @apply m-auto mb-3;
    }
    .teacher_box__rol {
        @apply mt-5 text-dh-black;
    }
    .teacher_box__name {
        @apply w-32 mx-auto font-bold uppercase;
    }
</style>
