  <template>
    <div class="container">
        <div v-for="(value,key) in tournaments" v-bind:key="'tournament-'+key">
            <h2 style="text-transform: uppercase;">{{key}}</h2>
            <b-list-group>
                <b-list-group-item button v-for="tournament in value" v-bind:key="'tournament-'+tournament.id">
                    <div @click='getMatches(tournament)' v-b-toggle="'collapse-'+tournament.id">
                        <b-container class="bv-example-row">
                            <b-row>
                                <b-col>{{tournament.name}}</b-col>
                            </b-row>
                        </b-container>
                    </div>
                    
                    <div class="text-center">
                        <b-icon v-if="loading && processId == tournament.id" icon="asterisk" animation="spin" font-scale="2"></b-icon>
                    </div>
                    <b-collapse :id="'collapse-'+tournament.id" class="mt-2">
                        <div v-if="!loading">
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
            tournaments: null,
            matches: null,
            loading: null,
            processId: null
        }
    },
    mounted() {
        this.getTournaments('http://localhost:8888/tournaments');
    },
    methods: {
        getTournaments: function(url) {
            Vue.axios.get(url).then((response) => {
                this.tournaments = response.data
                console.log(this.tournaments)
            })
        },
        getMatches: function(item) {
            console.log(item)
            this.processId = item.id
                this.loading = true
            Vue.axios.get('http://localhost:8888/matches').then((response) => {
                this.matches = response.data.matches
                this.loading = false
            })
        }
    }
}
</script>

