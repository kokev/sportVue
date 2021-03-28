  <template>
    <div class="container">
    <v-for>
        <div>
            <h2 style="text-transform: uppercase;">Torunament name{}</h2>
            <b-list-group>
                <b-list-group-item button>
                    <div @click='getMatches(29)' v-b-toggle="'collapse-1'">Toggle Collapse</div>
                    <b-icon v-if="loaded" icon="asterisk" animation="spin" font-scale="2"></b-icon>
                        <v-for>
                            <b-collapse id="collapse-1" class="mt-2" style="border-top: 2px solid black; background-color: #585858; margin: 0; padding: 10px; color: white;">
                                <b-container class="bv-example-row">
                                    <b-row class="text-center">
                                        <b-col><h4>Home team</h4></b-col>
                                        <b-col><h4>Away team</h4></b-col>
                                    </b-row>
                                    <hr style="border: 1px solid white;">
                                    <b-row class="text-center">
                                        <b-col>Home score</b-col>
                                        <b-col>-</b-col>
                                        <b-col>Away score</b-col>
                                    </b-row>
                                    <hr style="border: 1px solid white;">
                                    <p>Date 2020.20.20</p>
                                    <p>Comment</p>
                                </b-container>
                            </b-collapse>
                            <b-collapse id="collapse-1" class="mt-2" style="border-top: 2px solid black; background-color: #585858; margin: 0; padding: 10px; color: white;">
                            Match datas
                            </b-collapse>
                        </v-for>
                </b-list-group-item>
                                <b-list-group-item button>
                    <div  v-b-toggle="'collapse-2'">Toggle Collapse</div>
                        <b-collapse id="collapse-2" class="mt-2">
                        Match datas
                        </b-collapse>
                </b-list-group-item>
            </b-list-group>
        </div>
    </v-for>
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
        this.getTorunaments('https://cp.fn.sportradar.com/common/en/Etc:UTC/gismo/config_tournaments/1/17');
    },
    methods: {
        getTorunaments: function(url) {
            Vue.axios.get(url).then((response) => {
                this.torunaments = response
            })
        },
        getMatches: function(id) {
                this.loaded = true
            Vue.axios.get('https://cp.fn.sportradar.com/common/en/Etc:UTC/gismo/'+id+'/29/2021').then((response) => {
                this.matches = response
                this.loaded = false
            })
        }
    }
}
</script>

