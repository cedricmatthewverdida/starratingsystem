<template>
<Layout> 


   <v-container class="my-5">
            <v-card
                class="mx-auto"
            >
                <v-card-text>
                    
                    <h1 class="my-5 text-center caption">Star Rating System ~ <b>Cedric</b></h1>
                    
                    <v-row>

                        <v-col>


                            <h3 class="overline">Rate: <b> {{rating}}</b></h3>

                           

                            <v-rating
                                v-model="rating"
                                background-color="purple lighten-3"
                                color="purple"
                                half-increments
                                hover
                                large
                            ></v-rating>


                            <div class="my-5">
                                <h3>Overall rating</h3>

                                <h5>{{ overallround}} / 5</h5>
                                <v-rating
                                    color="amber"
                                    readonly
                                    size="30"
                                    length="5"
                                    half-increments
                                    :value="overall"
                                ></v-rating> 

                            </div>





                        </v-col>

                        <v-col>

                            
                                
                                
                                    <div
                                     v-for="(rates,i) in stars"
                                    :key ="i"
                                    >
                                    <sup> 
                                        <v-icon small>
                                          mdi-account
                                        </v-icon>
                                        {{rates.user}} &nbsp;
                                        <span class="red--text">({{rates.val}})</span>
                                    </sup>

                                       <v-rating
                                        color="amber"
                                        readonly
                                        size="30"
                                        length="5"
                                        :value="rates.key"
                                        ></v-rating> 
                                    </div>
                                

                                
                            

                        </v-col>

                    </v-row>


                </v-card-text>
                
                </v-card>
               
            </v-card>
    </v-container>

 


</Layout>
</template>

<script>
  export default {

    data: () => ({
      rating: 0,
      overall: 0,
      stars: [
        {
            key: 5,
            val: 0,
            user: 0
        },
        {
            key: 4,
            val: 0,
            user: 0
        },
        {
            key: 3,
            val: 0,
            user: 0
        },
        {
            key: 2,
            val: 0,
            user: 0
        },
        {
            key: 1,
            val: 0,
            user: 0
        }
        
      ]
    }),

    methods:{

        compute_star : function (){
            switch (this.rating){

                case 0.5:
                    case 1:
                this.calculate(1,this.rating)
                break;

                case 1.5:
                    case 2:
                this.calculate(2,this.rating)
                break;

                case 2.5:
                    case 3:
                this.calculate(3,this.rating)
                break;

                case 3.5:
                    case 4:
                this.calculate(4,this.rating)
                break;

                case 4.5:
                    case 5:
                this.calculate(5,this.rating)
                break;
            }
        },

        calculate : function (index,value) {
            var index = this.stars.findIndex(p => p.key == index)
            this.stars[index].val += value
            this.stars[index].user += 1
        },

        rates : function(){
            let rates = 0;
            let person_who_rates = 0;


            this.stars.forEach(element => {
                    if(element.val != 0){
                        rates += (element.key * element.user);
                        person_who_rates += element.user;
                    }
            });

            

           return Math.round((rates/person_who_rates) * 100) / 100
        }
    },

    computed: {

        overallround : function (){
            var multiplier = Math.pow(10, 1 || 0);
            return Math.round(this.overall * multiplier) / multiplier;
        }

    },
    watch:{
        rating : function (){
            this.compute_star();
            this.overall = this.rates();
        }
    }

  }
</script>
