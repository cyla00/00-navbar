<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'Navbar',
    props: {
        dark: Boolean,
    },
    setup(){
        return{
            scrollPosition: true,
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
            if(scroll > 50){
                this.scrollPosition = true
                return
            }
            this.scrollPosition = false
            return
        },
        scrollTop(){
            (document.getElementById('accueil') as any)?.scrollIntoView({ behavior: "smooth" })
        },
        async scrollService(){
            if(document.getElementById('services')){
                (document.getElementById('services') as any)?.scrollIntoView({ behavior: "smooth" })
                return
            }
            window.location.href = "/";
            return
        },
    },
    created(){
        window.addEventListener('resize', this.checkScreen)
        this.checkScreen()
        window.addEventListener('scroll', this.updateScroll)
    }
})
</script>


<template>
    <header :class="{'header-dark' : this.dark}">
        <meta name="header section" content="navigation menu with pages routes">
        <nav :class="{'mobile-nav': mobile}">
            <div class="logo-wrapper wrappers">
                <img src="https://placehold.jp/150x60.png" alt="main company logo">
            </div>

            <div class="links-wrapper">
                <router-link :class="{'a-dark' : this.dark}" to="/">route1</router-link>
                <router-link :class="{'a-dark' : this.dark}" to="/w">route2</router-link>
                <router-link :class="{'a-dark' : this.dark}" to="/a">route3</router-link>
                <router-link :class="{'a-dark' : this.dark}" class="btn-link" to="/"><button class="btn-router">button-route</button></router-link>
                <router-link :class="{'a-dark' : this.dark}" class="btn-link" to="/"><button class="btn-router">button-route</button></router-link>
            </div>
        </nav>
    </header>
</template>

<style scoped>
header{
    /* variables */
    --header-bg-dark: #26252C;
    --header-bg-light: #FEFEFE;
    --a-font-size: 14px;
    --a-text-color-dark: #777A84;
    --a-text-color-light: #747474;
    --a-text-color-active: #FF6D91;
    --a-text-color-bottom-border: #FF6D91;

    --btn-bg-color: trasparent;
    --btn-border-color: #007AFF;
    --btn-text-color: #FEFEFE;
    --btn-bg-color-hover: gray;
    --btn-text-color-hover: white;


    /* attributes */
    text-decoration: none;
    background: var(--header-bg-light);
    color: #1A1C1E;
    font-size: var(--a-font-size);
    position: sticky;
    top: 0;
    z-index: 99;
    width: 100%;
    background: #ffffff;
    transition: .2s ease all;
    margin: auto;
}
.header-dark{
    background: var(--header-bg-dark);
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
    text-decoration: none;
    color: var(--a-text-color-light);
    font-weight: bold;
    text-transform: uppercase;
    margin-left: 20px;
    border-bottom: 2px transparent;
    padding-block: 10px;
}
.a-dark{
    color: var(--a-text-color-dark);
}
a:hover {
    transition: 0.1s ease all;
    color: var(--a-text-color-active);
    border-bottom: solid 2px var(--a-text-color-bottom-border);
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
    color: var(--btn-text-color);
}
.btn-link{
    border: none !important;
}
.btn-router:hover{
    background: var(--btn-bg-color-hover);
    color: var(--btn-text-color-hover);
}
</style>
