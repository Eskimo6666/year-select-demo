<template>
    <section>
        <div class="fixed-selector">
            {{ currentItem }}
            <br/>
            <span v-for="(item,idx) in dataList" :key="idx" @click="scrollTo(idx)">{{item.year}}</span>
        </div>
        <div class="index-select-box" ref="indexBox">
            <cell v-for="(item,idx) in dataList" :key="idx" :cardData="item" />
        </div>
    </section>
</template>


<script>
import cell from './archCell.vue'
export default {
    name: 'index-select',
    components: { cell },
    data() {
        return {
            dataList: [
                { year: '2020', content: '2020' },
                { year: '2021', content: '2021' },
                { year: '2022', content: '2022' },
                { year: '2023', content: '2023' }
            ],
            // currentItem: '2020',
            active: 0
        }
    },
    computed: {
        currentItem() {
            return this.dataList[this.active].year
        }
    },
    mounted() {
        this.initScrollObserver()
    },
    methods: {
        initScrollObserver() {
            window.addEventListener('scroll', this.onScroll)
        },
        getScrollTop(el) {
            var top = 'scrollTop' in el ? el.scrollTop : el.pageYOffset; // iOS scroll bounce cause minus scrollTop

            return Math.max(top, 0);
        },
        onScroll() {
            let scrollTop = this.getScrollTop(window)
            let rects = []
            for (let i of this.$refs.indexBox.children) {
                let { height } = i.getBoundingClientRect()
                let top = i.offsetTop
                rects.push({ height, top })
            }
            this.active = this.getActiveIndex(scrollTop, rects)
            console.log(this.active, 47);
        },
        scrollTo(idx){
            var match = Array.from(this.$refs.indexBox?.children).filter((item,index)=>{
                console.log(item,index, '68');
                return index === idx
            })
            if(match[0]){
                match[0].scrollIntoView()
            }
            console.log(match);
        },
        getActiveIndex(scrollTop, rects) {
            for (let i = this.$refs?.indexBox?.children?.length - 1; i >= 0; i--) {
                // console.log(scrollTop, rects[i].top);
                if (scrollTop + 40 >= rects[i].top) {
                    return i
                }
            }
            return -1
        },
    }
}
</script>

<style scoped>
.fixed-selector {
    height: 40px;
    background-color: grey;
    color: red;
    position: fixed;
    top: 0;
    width: 100%;
}
</style>
