<script>
    import {ref} from "vue";
    import axios from "../service/axios.js";
    export default {
       setup(){
        const url = ref("")
        const shortenedUrl = ref("")
        const shorten = async() => {
            try{
                const {data} = await axios.post("/shorten", {
                    long_url: url.value.trim()
                })
                console.log(data.link)
                shortenedUrl.value = data.link
            }
            catch(err){
                console.log(err)
            }
        }
        return {shortenedUrl, shorten, url};
        },
    }
</script>

<template>
    <div>
        <form @submit.prevent="shorten">
            <input type="url" v-model="url"/>
            <button>Submit</button>
        </form>
        <a :href="shortenedUrl" target="_blank">{{shortenedUrl}}</a>
    </div>
</template>
