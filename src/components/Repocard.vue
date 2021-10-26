<template>
    <div class="repo-card">
        <div class="image-wrapper">
            <img src="" alt="">
        </div>
        <div class="description-wrapper">
            <b>{{repository.name}}</b>
            <p class="description"></p>
        </div>
        
    </div>
    <div v-if="isOpened">
        <code>
        {{repository}}
        </code>
    </div>
</template>

<script>
export default {
  data () {
    return {
        isOpened: false,
    }
  },
    props: ['repository'],
    name: "Repocard",
}
</script>

<style lang="less">
    @iconSize : 100px;

    .repo-card{
        padding: 20px;
        width: 100%;
        display: flex;
        flex-direction: row;
        gap: 20px;
        border-radius: 10px;
        border: 1px solid #3b3b3b;
        transition: 0.3s ease-in-out;
        &:hover{
            -webkit-box-shadow: 0px 0px 15px 0px rgba(255,255,255,0.1); 
            box-shadow: 0px 0px 15px 0px rgba(255,255,255,0.1);
        }
        .description{
            display: -webkit-box;
            line-clamp: 3;
            height: 3.5rem;
            overflow: hidden;
            -webkit-line-clamp: 3;
            text-overflow: ellipsis;
        }
    }
    .image-wrapper{
        width: @iconSize;
        height: @iconSize;
        min-width: @iconSize;
        border-radius: 8px;
        border: 1px solid #3b3b3b9a;
    }
</style>