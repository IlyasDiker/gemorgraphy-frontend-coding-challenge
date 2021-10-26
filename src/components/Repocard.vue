<template>
    <div class="repo-card">
        <div class="card-content">
            <div class="image-wrapper">
                <img :src="repository.owner.avatar_url" alt="">
            </div>
            <div class="description-wrapper">
                <b>{{repository.name}}</b>
                <p class="description" v-if="repository.description">{{repository.description}}</p>
                <div class="card-tools">
                    <div class="tool" title="Stargazers">
                        <i class='bx bx-star'></i>
                        <div class="show-on-hover">
                            <label>Stargazers:</label>
                        </div>
                        <span>{{repository.stargazers_count}}</span>
                    </div>
                    <div class="tool" title="Issues">
                        <i class='bx bx-bug'></i>
                        <div class="show-on-hover">
                            <label>Issues:</label>
                        </div>
                        <span>{{repository.open_issues_count}}</span>
                    </div>
                </div>
            </div>
            <div class="flex-row gap-5">
                <button v-on:click="isOpened = !isOpened" class="rounded icon"><i class='bx bx-chevron-down'></i></button>
                <button v-on:click="logselected()" class="rounded icon"><i class='bx bx-code-block' ></i></button>
            </div>
        </div>
        <footer v-if="isOpened" class="card-footer">
            <code>
            {{repository}}
            </code>
        </footer>
    </div>
</template>

<script>
export default {
    props: {
        repository: null,
    },
    methods: {
        logselected: () => {
            console.log("Logged Item : ", this.repository)
        }
    },
    data () {
        return {
            isOpened: false,
        }
    },
    
    name: "Repocard",
}
</script>

<style lang="less">
    @import '../assets/global';
    @iconSize : 100px;

    .repo-card{
        width: 100%;
        display: flex;
        flex-direction: column;
        
        border-radius: 10px;
        border: 1px solid #3b3b3b;
        transition: 0.3s ease-in-out;
        &:hover{
            -webkit-box-shadow: 0px 0px 15px 0px rgba(255,255,255,0.1); 
            box-shadow: 0px 0px 15px 0px rgba(255,255,255,0.1);
        }
        .description{
            display: -webkit-box;
            text-overflow: ellipsis;
        }
        .card-content{
            gap: 20px;
            padding: 20px;
            display: flex;
            flex-direction: row;
        }
        .card-footer{
            transition: 0.2s ease-in-out;
            padding: 20px;
            background: #1b1b1b;
            font-size: 10px;
            max-height: 300px;
            overflow-y: auto;
            animation: slide 1s ease 3.5s forwards;
        }
        .card-tools{
            display: flex;
            flex-direction: row;
            gap: 10px;
            .tool{
                color: white;
                opacity: .7;
                transition: 0.2s ease-in-out;
                border: 1px solid #3b3b3b;
                border-radius: 50px;
                padding: 5px 8px;
                display: flex;
                width: fit-content;
                transition: all 0.5s ease-in-out;
                flex-direction: row;
                cursor: default;
                &:hover{
                    opacity: 1;
                    width: fit-content;
                    .show-on-hover{
                        opacity: 1;
                        max-width: 100%;
                    }
                }
                .show-on-hover{
                    opacity: 0;
                    transition: 0.5s ease-in-out;
                    transform-origin:left;
                    width: fit-content;
                    max-width: 0;
                    overflow: hidden;
                }
                label{
                    opacity: .7;
                    margin-right: 5px;
                }
                i{
                    margin-right: 8px;
                }
            }
        }
    }
    .image-wrapper{
        width: @iconSize;
        height: @iconSize;
        min-width: @iconSize;
        border-radius: 8px;
        border: 1px solid #3b3b3b9a;
        overflow: hidden;
        img{
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
    }
    .description-wrapper{
        display: flex;
        flex-direction: column;
        flex-grow: 1;
        gap: 10px;
        p{
            font-size: 0.9rem;
            max-width: 500px;
            color: rgb(180, 180, 180);
        }
    }

    @keyframes slide {
        from {height: 0;}
        to {height: 300px;}
    }

</style>