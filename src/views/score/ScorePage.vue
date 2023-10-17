<script setup>
import Config from '@/config.json';
import { useRoute } from 'vue-router';
const id = 1;
const route = useRoute();
const userid = route.params.id;

startLoading();
setTitle("Loading...");

fetch(`${Config.apiUrl}/user/${id}`).then(res => res.json()).then(data => {
    if (!data.data) {
        stopLoading();
        react.loading = false;
        return;
    }
    react['user'] = data.data;
    stopLoading();
    react.loading = false;
}).catch(err => {
    console.error(err);
    stopLoading();
});

setTitle("Score Page");

</script>

<template>
    <div class = "scoreCard">
        <img :src="Config.apiUrl + '/assets/cover/' + id" class="banner" alt="song">
        <div class = "songInfo">
            <p class = "title">Paradigm Shift by Morimori Atsushi</p>
            <p class = "title">25.6 + DT HD FC - New Paradigm by fluXis</p>
        </div>

        <div class = "playerInfo">
            <div class = "textContainer">
                <p class = "title">Played by KaneryU</p>
                <p class = "title">Rank a</p>
            </div>
            <img :src="Config.apiUrl + '/assets/avatar/' + userid" class="profile" alt="user banner">

        </div>
    </div>
</template>

<style lang = "scss">

.scoreCard{
    width: 1303px;
    height: 320px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: none;
    border-radius: 20px;
    overflow: hidden;

    .banner{
        width: 1303px;
        height: 430px;
        object-fit: cover;
        border-radius: 20px 20px 0 0;
        opacity: 50%;
        filter: blur(10px);
        -webkit-filter: blur(10px);
    }

    .songInfo {
        display: flex;
        width: 636px;
        padding: 9px;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        gap: -20px;
        top: 0px;
        right: 667px;
        position: absolute;

        .title {
            font-family: Renogare Soft;
            font-size: 21px;
            font-style: normal;
            font-weight: 400;
            line-height: normal;
            
            color: #FFF;
            text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);


        }

    }

    .playerInfo {
        display: flex;
        padding: 9px;
        justify-content: flex-end;
        align-items: flex-start;
        gap: 10px;

        position: absolute;
        right: 0px;
        top: -0.5px;

        .title {
            font-family: Renogare Soft;
            font-size: 21px;
            font-style: normal;
            font-weight: 400;
            line-height: normal;
            
            color: #FFF;
            text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);


        }

        .textContainer{
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: flex-end;
            gap: 10px;
        }

        .profile{
            width: 103px;
            height: 103px;
            border-radius: 20px;
            margin-right: 10px;
            object-fit: cover;
            box-shadow: var(--box-shadow);
        }

    }

}





</style>