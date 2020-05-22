<template>
    <section>
        <div v-if="type != 'character'" class="results results_anime">

            <div 
                class="card" 
                v-for="(item,index) in data" 
                :key="index">

                <div class="img_container">
                    <div class="img">
                        <img :src="item.image_url" :alt="item.title">
                    </div>
                    <div class="img_info">
                        <a :href="item.url" target="_blank">Details</a>
                    </div>
                </div>

                <div class="info_container">

                    <div class="info_title">{{item.title}}</div>
                    <div class="info_synopsis">{{item.synopsis}}</div>
                    <div class="info_details">

                        <div class="info_details_dates">
                            <span>Start Date: {{ fixDate(item.start_date) }}</span>
                            <span>End Date: {{ fixDate(item.end_date) }}</span>
                        </div>

                        <div class="info_details_extra">
                            <span>Score: {{ item.score }}</span>
                            <span>Rated: {{ item.rated }}</span>
                        </div>

                    </div>

                </div> 

            </div>

        </div>

        <div v-if="type == 'character'" class="results results_character">

            <div 
                class="card_character" 
                v-for="(item,index) in data" 
                :key="index">

                <div class="info_title">{{item.name}}</div>

                <div class="img">
                    <img :src="item.image_url" :alt="item.title">
                </div>

                <div class="img_info">
                    <a :href="item.url" target="_blank">Details</a>
                </div>

            </div>

        </div>
    </section>

</template>

<script>
export default {
    props:[
        "data",
        "type"
    ],

    methods: {
        fixDate(el){
            if (typeof el == "string") {
                let date = el.split('T')
                date = date[0].split('-')
                date = `${date[1]}/${date[2]}/${date[0]}`
                return date
            }
            return 'uknkown'
        }
    },
}
</script>

<style>
    .results{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-between;
    }

    .card{
        border-radius: 12px;
        border: 2px solid rgba(255, 255, 255, .5);
        background: rgba(0, 0, 0, 1);
        width: 48%;
        margin: 40px 0;
        padding: 10px 20px;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    .card .img_container{
        width: 30%;
        display: flex;
        flex-direction: column;
    }

    .card .img_container .img_info{
        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }

    .card .img_container .img_info a{
        width: 80px;
        padding: 5px 10px;
        margin: 0 auto;
        border-radius: 3px;
        text-align: center;
        text-decoration: none;
        color: #fff;
        background: #4f6d44;
    }

    .card .img_container .img img{
        border-radius: 12px;
        width: 100%;
    }

    .card .info_container{
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        width: 65%;
    }

    .card .info_container .info_title{
        text-align: center;
        font-weight: 700;
        font-size: 20px;
        margin-bottom: 5px;
    }

    .card .info_container .info_synopsis{
        text-align: justify;
        font-size: 18px;
    }

    .card .info_container .info_details{
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        font-size: 16px;
    }

    .card .info_container .info_details .info_details_dates,
    .card .info_container .info_details .info_details_extra{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        font-weight: 300;
        text-align: end;
    }

    .card_character{
        width: 18%;
        margin: 40px 0;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
    }

    .card_character .img_info{
        margin-top: 15px;
    }

    .card_character .img img{
        border-radius: 12px;
    }

    .card_character .img_info a{
        width: 100px;
        padding: 10px 15px;
        border-radius: 3px;
        font-size: 18px;
        text-align: center;
        text-decoration: none;
        color: #fff;
        background: #4f6d44;
    }

    .card_character .info_title{
        text-align: center;
        font-weight: 700;
        font-size: 20px;
        margin-bottom: 5px;
    }

    @media screen and (max-width: 1200px){
        .card{
            width: 49%;
        }
        
        .card .img_container{
            width: 24%;
        }

        .card .info_container{
            width: 73%;
        }
        
        .card_character{
            width: 25%;
        }
    }

    @media screen and (max-width: 1150px){
        .card{
            margin: 0 auto;
            margin-top: 20px;
            width: 80%;
        }
    }

    @media screen and (max-width: 1000px){
        .card{
            margin: 0 auto;
            margin-top: 20px;
            width: 80%;
        }
    
        .card_character{
            width: 28%;
        }
    }

    @media screen and (max-width: 700px){
        .card{
            margin: 0 auto;
            margin-top: 20px;
            width: 100%;
        }

        .card_character{
            width: 45%;
        }
    }

    @media screen and (max-width: 525px){

        .card{
            flex-direction: column;
            justify-content: space-between;
        }

        .card .img_container{
            margin: 0 auto;
            width: 50%;
        }

        .card .info_container{
            margin-top: 20px;
            width: 100%;
        }

        .card .info_container .info_details .info_details_dates{
            margin-top: 15px;
            flex-direction: column;
            text-align: center;
        }

        .card .info_container .info_details .info_details_extra{
            margin-top: 5px;
            justify-content: space-around;
        }

        .card_character{
            margin: 20px auto;
            width: 80%;
        }
    }

</style>