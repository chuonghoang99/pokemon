<template>
    <div class="card">
        <div
            class="card__inner"
            @click="onTogle()"
            :class="{ 'is-flipped': isFlip }"
        >
            <div class="card__face card__font">
                <div class="card__content" :style="setFontImage"></div>
            </div>
            <div class="card__face card__back">
                <div class="card__content"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        prop_card: {
            type: Object,
            require: true,
        },
    },
    data() {
        return {
            isFlip: false,
            isDisable: false,
        }
    },
    computed: {
        setFontImage() {
            return {
                //   backgroundColor: 'red',
                backgroundImage: `url(${require(`@/assets/images/${this.prop_card.value}.png`)})`,
            }
        },
    },
    methods: {
        onTogle() {
            if (this.isDisable) return
            this.isFlip = !this.isFlip
            if (this.isFlip) {
                this.$emit('onFlip', this.prop_card)
            }
        },
        closeFlip() {
            this.isFlip = false
        },
    },
}
</script>

<style lang="css" scoped>
.card {
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
    width: 90px;
    height: 120px;
}

.card__inner {
    width: 100%;
    height: 100%;
    transition: transform 1s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
}

.card__inner.is-flipped {
    transform: rotateY(180deg);
}

.card__face {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    box-shadow: 0 3px 5px 3px rgba(0, 0, 0, 0.2);
}

.card__font {
    background-color: var(--light);
    transform: rotateY(180deg);
}

.card__font .card__content {
    background-color: var(--dark);
    background-size: contain;
    background-position: center center;
    background-repeat: no-repeat;
    width: 100%;
    height: 100%;
}
.card__back .card__content {
    background: url('../assets/images/icon_back.png') no-repeat center center;
    background-size: 40px 40px;
    height: 100%;
    width: 100%;
}
</style>
