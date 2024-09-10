<script setup>
import heart from '~/static/icons/heart.svg'
import star from '~/static/icons/star.svg'
import cross from '~/static/icons/cross.svg'
</script>
<template>
    <div class="control">
        <div class="control__btn control__btn_deny"><img :src="cross"></div>
        <div class="control__btn control__btn_super"><img :src="star"></div>
        <div class="control__btn control__btn_accept"><img :src="heart" ></div>
    </div>
</template>
<style lang="scss">

.control {
    display: flex;
    justify-content: space-around;
    width: 100%;
    &__btn {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 56px;
        height: 56px;
        border-radius: 1000px;
        border: 1px solid;

        &_accept {
            border-color: #2fd52f;
            img {
                width: 36px;
                height: 36px;
            }          
        }

        &_deny {
            border-color: #EA4080;
            img {
                width: 36px;
                height: 36px;
            }
        }

        &_super {
            border-color: #62BAF3;
            img {
                width: 36px;
                height: 36px;
            }          
        }
    }
}
</style>