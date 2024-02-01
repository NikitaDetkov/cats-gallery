<template>
    <div class="header">
        <div class="header__item">
            <nuxt-link class="header__item--link" exact no-prefetch active-class="active" to="/">Все котики</nuxt-link>
        </div>
        <div class="header__item">
            <nuxt-link class="header__item--link" exact no-prefetch active-class="active" to="/favourites">Любимые котики</nuxt-link>
        </div>
    </div>
</template>

<style scoped>
    .header {
        padding: 0;
        margin: 0;
        display: flex;
        background-color: #2196F3;
        box-sizing: border-box;
        padding: 0 62px;
        box-shadow: 0px 4px 4px 0px #0000003D;
    }

    .header__item {
        display: flex;
    }

    .header__item--link {
        height: 64px;
        display: flex;
        text-decoration: none;
        color: white;
        align-items: center;
        justify-content: center;
        text-align: center;
        padding: 0 22px;
        cursor: pointer;
        opacity: 0.7;
        font-family: Roboto;
        font-size: 14px;
        font-weight: 400;
        line-height: 21px;
        letter-spacing: 0.25px;
        text-align: center;
    }

    .header__item--link.active {
        opacity: 1;
        background-color: #1E88E5;
    }
</style>