  <template>
    <div class="container">
        <div>
            <h2 style="text-transform: uppercase;">Torunament name{}</h2>
            <b-list-group>
                <b-list-group-item button>
                    <div @click='getMatches()' v-b-toggle="'collapse-1'">
                        <b-container class="bv-example-row">
                            <b-row>
                                <b-col>Tournament name</b-col>
                            </b-row>
                        </b-container>
                    </div>
                    <b-icon v-if="loaded" icon="asterisk" animation="spin" font-scale="2"></b-icon>
                            <b-collapse id="collapse-1" class="mt-2">
                                <div v-for="match in matches" v-bind:key="match.id" 
                                style="border-top: 2px solid black; background-color: #585858; 
                                margin-bottom: 10px; padding: 10px; color: white;">
                                    <b-container class="bv-example-row">
                                        <b-row class="text-center">
                                            <b-col><h4>{{match.home_team}}</h4></b-col>
                                            <b-col><h4>{{match.away_team}}</h4></b-col>
                                        </b-row>
                                        <hr style="border: 1px solid white;">
                                        <b-row class="text-center">
                                            <b-col>{{match.home_score}}</b-col>
                                            <b-col>-</b-col>
                                            <b-col>{{match.away_score}}</b-col>
                                        </b-row>
                                        <hr style="border: 1px solid white;">
                                        <p>{{match.date}} {{match.time}}</p>
                                        <p>{{match.comment}}</p>
                                    </b-container>
                                </div>
                            </b-collapse>
                </b-list-group-item>
            </b-list-group>
        </div>
    </div>
</template>

<script>
import Vue from 'vue';

export default {
    name: 'Home',
    data () {
        return {
            torunaments: null,
            matches: null,
            loaded: null
        }
    },
    mounted() {
        this.getTorunaments('http://localhost:8888/tournaments');
    },
    methods: {
        getTorunaments: function(url) {
            Vue.axios.get(url).then((response) => {
                this.torunaments = response
            })
        },
        getMatches: function() {
                this.loaded = true
            Vue.axios.get('http://localhost:8888/matches').then((response) => {
                this.matches = response.data.matches
                this.loaded = false
            })
        }
    }
}
</script>

