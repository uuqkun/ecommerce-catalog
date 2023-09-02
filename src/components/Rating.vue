<script>
export default {
    name: "Rating",
    props: {
        rate: Number,
        dotBgColor: Array
    },
    methods: {
        getRatingBg() {
            // split between integer and decimal number from rating
            const parsedInt = parseInt(this.rate)
            const decimal = Math.round((this.rate - parsedInt) * 10) / 10

            const div = document.querySelectorAll('.dot-bg');
        
            for (let i = 0; i < div.length; i++) {
                const dotBg = div[i];
                
                if (i < parsedInt) {
                    dotBg.classList.add('filler')
                    dotBg.style.width = `100%`
                } else if (i === parsedInt) { // 3 === 
                    dotBg.style.width = `${decimal * 100}%`
                } else if (i > parsedInt) {
                    dotBg.classList.remove('filler');
                    dotBg.style.width = `0`
                }
            }
        }
    },
    mounted() {
        this.getRatingBg();
    }, 
    updated () {
        this.getRatingBg();
    }
}
</script>

<template>
    <div class="rating__indicator flex">
        <div class="rating__indicator-value">
            <p class="text-subheader">
                {{ rate }}/5
            </p>
        </div>

        <div :class="[, 'rating__indicator-ellipse flex']">
            <span>
                <div :class="[dotBgColor, 'dot-bg']" />
            </span>
            <span>
                <div :class="[dotBgColor, 'dot-bg']" />
            </span>
            <span>
                <div :class="[dotBgColor, 'dot-bg']" />
            </span>
            <span>
                <div :class="[dotBgColor, 'dot-bg']" />
            </span>
            <span>
                <div :class="[dotBgColor, 'dot-bg']" />
            </span>
        </div>
    </div>
</template>

<style scoped>
.rating__indicator {
    gap: 1rem;
}

.rating__indicator-ellipse {
    gap: .25rem;
}

.rating__indicator-ellipse span {
    width: 18px;
    height: 18px;
    border: 1px solid black;
    border-radius: 50%;

    position: relative;
    overflow: hidden;
}

.dot-bg { 
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
}

.filler {
    width: 100%;
}
</style>