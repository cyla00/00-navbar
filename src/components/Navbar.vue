<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'Navbar',
    props: {
        dark: Boolean,
    },
    data(){
        return{
            scrollPosition: false,
            mobile: false,
            mobileNav: false,
            windowWidth: 0,
        }   
    },
    methods: {
        toggleMobileNav(){
            this.mobileNav = !this.mobileNav
        },
        checkScreen(){
            this.windowWidth = window.innerWidth
            if(this.windowWidth <= 1050){
                this.mobile = true      
                return
            }
            this.mobile = false
            this.mobileNav = false
            return
        },
        updateScroll(){
            const scroll = window.scrollY
            if(scroll > 0){
                this.scrollPosition = true
                return
            }
            this.scrollPosition = false
            return
        },
    },
    created(){
        this.checkScreen()
        window.addEventListener('resize', this.checkScreen)
        window.addEventListener('scroll', this.updateScroll)
    }
})
</script>


<template>
    <header :class="{'header-dark': this.dark, 'scrolled-nav': scrollPosition, 'mobile-size': mobile}">
        <meta name="header section" content="navigation menu with pages routes">

        <nav :class="{'mobile-nav': mobile}">
            <div class="logo-wrapper wrappers" v-show="!mobile">
                <img class="logo-image" src="https://placehold.jp/100x50.png" alt="main company logo">
            </div>

            <div class="links-wrapper" v-show="!mobile">
                <router-link :class="{'a-dark' : this.dark}" to="/">route1</router-link>
                <router-link :class="{'a-dark' : this.dark}" to="/">route2</router-link>
                <router-link :class="{'a-dark' : this.dark}" to="/">route3</router-link>
                <router-link class="btn-link" to="/"><button :class="{'btn-dark' : this.dark}" class="btn-router">button-route</button></router-link>
                <router-link class="btn-link" to="/"><button :class="{'btn-dark' : this.dark}" class="btn-router">button-route</button></router-link>
            </div>

            <div class="icon" :class="{'icon-dark': this.dark}">
                <i @click="toggleMobileNav" v-show="mobile" class='bx bx-menu bx-md' :class="{'icon-active': mobileNav}"></i>
            </div>

            <Transition name="mobile-nav">
                <div class="mobile-links-wrapper" v-show="mobileNav" :class="{'mobile-links-wrapper-dark' : this.dark}">
                    <div class="logo-wrapper wrappers" v-show="mobile">
                        <img class="mobile-logo-image" src="https://placehold.jp/100x50.png" alt="main company logo">
                    </div>
                    <router-link class="btn-link" to="/"><button :class="{'btn-dark' : this.dark}" class="btn-router">button-route</button></router-link>
                    <router-link class="btn-link" to="/"><button :class="{'btn-dark' : this.dark}" class="btn-router">button-route</button></router-link>
                    <router-link :class="{'a-dark' : this.dark}" to="/">route1</router-link>
                    <router-link :class="{'a-dark' : this.dark}" to="/">route2</router-link>
                    <router-link :class="{'a-dark' : this.dark}" to="/">route3</router-link>
                </div>
            </Transition>
        </nav>
    </header>
</template>

<style scoped>
header{
    /* variables */
    --header-bg-dark: #0D1520;
    --header-bg-light: #FEFEFE;
    --a-font-size: 14px;
    --a-text-color-dark: #FEFEFE;
    --a-text-color-light: #0D1520;
    --a-text-color-active: #9E76E8;
    --a-text-color-bottom-border: #80838C;

    --btn-bg-color: trasparent;
    --btn-border-color: #EA48BA;
    --btn-text-color-dark: #FEFEFE;
    --btn-text-color-light: #FEFEFE;
    --btn-bg-color-hover: #9E76E8;
    --btn-text-color-hover: #FEFEFE;
    --btn-text-color-dark: #0D1520;


    /* attributes */
    text-decoration: none;
    background: var(--header-bg-light);
    color: #1A1C1E;
    font-size: var(--a-font-size);
    position: sticky;
    top: 0;
    z-index: 99;
    background: #ffffff;
    transition: 0.2s ease all;
    margin: auto;

    width: 90%;
    border-radius: 100px;
    margin-top: 10px;
}
.header-dark{
    background: var(--header-bg-dark);
}
.scrolled-nav{
    transition: 0.2s ease all;
    width: 100%;
    border-radius: 0;
    margin-top: 0;
}
.links-wrapper{
    margin: auto;
    margin-right: 0;
}

nav{
    display: flex;
    flex-direction: row;
    height: 100%;
    padding: 5px 0;
    transition: 0.2s ease all;
    width: 90%;
    position: relative;
    margin: 0 auto;
    @media(min-width: 1140px) {
        max-width: 1140px;
    }
}


a{
    transition: 0.2s ease all;
    text-decoration: none;
    color: var(--a-text-color-light);
    font-weight: bold;
    text-transform: uppercase;
    margin-left: 20px;
    border-bottom: 1px transparent;
    padding-block: 5px;
}
.a-dark{
    color: var(--a-text-color-dark);
}
a:hover {
    transition: 0.2s ease all;
    color: var(--a-text-color-active);
    border-bottom: solid 1px var(--a-text-color-bottom-border);
}
a.router-link-exact-active {
    transition: 0.2s ease all;
    color: var(--a-text-color-active);
}


.btn-router{
    transition: 0.2s ease all;
    font-weight: bold;
    text-transform: uppercase;
    padding: 10px;
    border: solid 2px var(--btn-border-color);
    outline: none;
    border-radius: 100px;
    cursor: pointer;
    background: var(--btn-bg-color);
    color: var(--btn-text-color-dark);
}
.btn-link{
    border: none !important;
}
.btn-router:hover{
    background: var(--btn-bg-color-hover);
    color: var(--btn-text-color-hover);
}
.btn-dark{
    color: var(--btn-text-color-light);
}
.logo-image{
    margin: auto;
    display: block;
}

.icon{
	display: flex;
	top: 0;
	align-items: center;
	right: 24px;
	height: 100%;
	color: var(--a-text-color-light);
    padding: 5px;
    margin: 10px;
    border-radius: 100px;
}
.icon-dark{
    color: var(--a-text-color-dark);
}
.icon-active{
	transform: rotate(180deg);
}
.mobile-nav{
    justify-content: flex-end;
}
.mobile-links-wrapper{
	display: flex;
	flex-direction: column;
	position: fixed;
	width: 100%;
	max-width: 250px;
	height: 100%;
	background: var(--header-bg-light);
	top: 0;
	left: 0;
	margin: 0;
    border-radius: 0px 20px 20px 0px;
}
.mobile-links-wrapper a{
    margin-top: 15px;
    border: none;
    margin-inline: auto;
}
.mobile-logo-image{
    margin-top: 30px;
}

.mobile-links-wrapper-dark{
	background: var(--header-bg-dark);
}


.mobile-nav-enter-active, .mobile-nav-leave-active {
	transition: 0.6s ease all;
}
.mobile-nav-enter-from, .mobile-nav-leave-to {
	transform: translateX(-300px);
}
.mobile-nav-enter-to {
	transform: translateX(0);
}
</style>
