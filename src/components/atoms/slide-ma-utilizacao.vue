<style scoped lang="sass">
    @import ../../sass/imports/_extend

    #internal
        position: relative
        height: 80%
        width: 75%
        border-radius: $pixel-proportion / 2
        +flex(row, n, center, center)

        > .box
            width: 100%
            height: 100%
            background-color: $transparent
            box-shadow: none
            border: none
            +flex(column, n, center, center)

            > h1,
            > h2
                color: $white
                text-shadow: 0 0 30px $black

            > h2
                font-weight: 900
                font-size: 60px

            > h1
                font-weight: 900
                font-size: 90px
                line-height: 70px

</style>

<template lang="pug">
    #internal
        .box
            h2.subtitle.is-1.is-marginless Bla bla bla...
            h1.subtitle.is-1.is-marginless.has-text-centered
                | Minha empresa
                br
                | fica aqui...
</template>

<script>
    import { mapState, mapGetters, mapActions } from 'vuex'

    export default {
        props: [],
        data: () => ({
            info: {
                id: 'ma-utilizacao',
                light: {
                    cameraTracking: true
                },
                coordinates: {
                    latitude: -12.13479271004742,
                    longitude: -39.35211653166833
                },
                scale: 10000,
                camera: {
                    tilt: 75,
                    heading: 0
                },
                basemap: 'satellite',
                symbol: {
                    width: 350,
                    height: 500,
                    primitive: 'inverted-cone',
                    color: '#E1392F'
                },
                point: {
                    x: -39.34545,
                    y: -12.1284,
                    z: 250
                }
            }
        }),
        mounted: function () {
            this.checkSlide()
        },
        computed: {
            ...mapGetters([
                'slides'
            ]),
            ...mapState({
                actual: state => state.app.actual
            })
        },
        methods: {
            ...mapActions([
                'actualSlide'
            ]),
            checkSlide () {
                const slide = this.slides[this.actual]
                if (slide === this.info.id) {
                    this.actualSlide(this.info)
                }
            }
        }
    }
</script>
