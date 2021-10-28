<template>
    <nav class="navbar">
        <span class="navbar-logo">Gemophraphy-frontend-challenge</span>
        <div class="select-mode">
            <!-- Pagination Mode -->
            <div>
                <button 
                    :class="{active: paginationMode == 'LOAD_MORE'}"
                    v-on:click="changeMode('LOAD_MORE')"
                    >Load More</button>
                <button 
                    :class="{active: paginationMode == 'PAGES'}"
                    v-on:click="changeMode('PAGES')"
                    >Pages</button>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    name: "Navbar",
    data () {
        return {
            paginationMode: 'LOAD_MORE',
        }
    },
    methods: {
        changeMode (pMode) {
            this.paginationMode = pMode;
            this.$emit("selectedMode", this.paginationMode);
        }
    },
}
</script>

<style lang="less">
    .navbar{
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        padding: 20px;
        color: white;
        background: rgba(0, 0, 0, 0.445);
        backdrop-filter: blur(20px);
        -webkit-backdrop-filter: blur(20px);
        border-bottom: 1px solid rgba(245, 245, 245, 0.247);
        z-index: 99;
        display: flex;
        align-items: center;
        flex-direction: row;
        justify-content: space-between;
        .navbar-logo{
            font-size: 1rem;
        }
    }
    .select-mode{
        display: flex;
        flex-direction: column;
        flex-wrap: nowrap;
        background: rgba(128, 128, 128, 0.185);
        border-radius: 100px;
        overflow: hidden;
        button{
            border-radius: 100px;
            border: 0px;
            padding: 5px 10px;
            &:hover{
                background: transparent;
            }
            &.active{
                &:hover{
                    background: #3d3d3d;
                }
            }
        }
        label{
            font-size: 12px;
            opacity: .7;
            margin-bottom: 5px;
        }
    }
</style>