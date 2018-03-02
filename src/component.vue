<template>
    <!-- Slider main container -->
    <div ref="swiper" class="swiper-container">
        <!-- Additional required wrapper -->
        <div class="swiper-wrapper">
            <!-- Slides -->
            <slot>

            </slot>
        </div>
        <!-- If we need pagination -->
        <div ref="pagination_div" v-if="pagination" class="swiper-pagination"></div>

        <!-- If we need navigation buttons -->
        <div ref="btn_prev" v-if="button" class="swiper-button-prev"></div>
        <div ref="btn_next" v-if="button" class="swiper-button-next"></div>

        <!-- If we need scrollbar -->
        <div ref="scrollbar_div" v-if="scrollbar" class="swiper-scrollbar"></div>
    </div>
</template>
<style scoped>
    @import "../node_modules/swiper/dist/css/swiper.min.css";
</style>

<script>
    import Swiper from '../node_modules/swiper/dist/js/swiper.min'
    // 注册
    export default {
        name: 'vue-smart-swiper',
        // 声明 props
        props: {
            pagination: {
                type: Boolean,
                default: false
            },
            button: {
                type: Boolean,
                default: false
            },
            scrollbar: {
                type: Boolean,
                default: false
            },
            option: {
                type: Object,
                default: function () {
                    return { // Optional parameters
                        // direction: 'vertical',
                        loop: true,

                        // If we need pagination
                        pagination: {
                            el: '',
                        },

                        // Navigation arrows
                        navigation: {
                            nextEl: '',
                            prevEl: '',
                        },

                        // And if we need scrollbar
                        scrollbar: {
                            el: '',
                        }
                    }
                }
            }
        },
        data: function () {
            return {swiper: null}
        },
        beforeDestroy: function () {
            this.swiper.destroy(true, true)
        },
        mounted: function () {
            let self = this;
            this.$nextTick(function () {
                self.option.pagination = {el: this.$refs.pagination_div};
                self.option.navigation = {nextEl: this.$refs.btn_next, prevEl: this.$refs.btn_prev};
                self.option.scrollbar = {el: this.$refs.scrollbar_div};

                let init_fuc
                if (self.option && self.option.on && self.option.on.init) {
                    init_fuc = self.option.on.init
                } else {
                    init_fuc = false
                }
                self.option.init = false;
                self.swiper = new Swiper(self.$refs.swiper, self.option)
                self.swiper.on('init', function () {
                    if (init_fuc) {
                        init_fuc(self.swiper)
                    }
                    self.$emit('init', self.swiper)
                });
                let events = ['beforeDestroy', 'slideChange', 'slideChangeTransitionStart', 'slideChangeTransitionEnd', 'slideNextTransitionStart', 'slideNextTransitionEnd', 'slidePrevTransitionStart', 'slidePrevTransitionEnd', 'transitionStart', 'transitionEnd', 'touchStart', 'touchMove', 'touchMoveOpposite', 'sliderMove', 'touchEnd', 'click', 'tap', 'doubleTap', 'imagesReady', 'progress', 'reachBeginning', 'reachEnd', 'fromEdge', 'setTranslate', 'setTransition', 'resize'];

                for (let i = 0; i < events.length; i++) {
                   let e = events[i];
                    function callback(param) {
                        self.$emit(e.toLowerCase(), self.swiper, param)
                    }
                    self.swiper.on(e, callback)
                }

                self.swiper.init()

            })
        }
    }
</script>