<template>
        <div onload="beforeMount()">
            <div class="sel">
                <div @click="ShowFirst()"><input type="text" v-model="maininput"/></div>
                <div
                        @click="reset()"
                >❌</div>
            </div>
            <div class="inp" v-if="first">
                <div class="sersel">
                    <div
                            @click="maininputall()"
                        >Select all
                    </div>
                    <div>
                        <input v-model="searchvalue" class="search" placeholder="Search"/>
                    </div>
                </div>
                <ElementList
                        v-for="elem of SearchFun"
                        :key="elem.id"
                        @click="elemminus(elem)"
                        v-bind:class="{active: elem.selected}"
                        v-bind:elem="elem"
                />
                <div>
                    <button style="width: 100%" @click="PostVid">Aply</button>
                </div>
            </div>
        </div>
</template>
<script>
import axios from 'axios'
import ElementList from '@/components/ElementList.vue'
export default {
    name: 'FormIn',
    components: {
        ElementList
    },
    data(){
        return{
            categories: [],
            errors: [],
            first: false,
            searchvalue: '',
            maininput:''
        }
    },
    methods: {
        ShowFirst() {
            this.first = !this.first;
        },
        reset (){
            this.maininput = ' ';
            this.first = !this.first;
            var max = this.categories.length;
            for (var i = 0; i < max; i++) {
            this.categories[i].selected = false;
            }
        },
        maininputall() {
            this.maininput = ' ';
            var max = this.categories.length;
            for (var i = 0; i < max; i++) {
                this.categories[i].selected = true;
                this.maininput = this.maininput + ' ' + this.categories[i].name;
            }
        },
        elemminus (elem){
            this.categories[elem.id].selected = !this.categories[elem.id].selected;
            if (this.categories[elem.id].selected === false)
            {this.maininput = this.maininput.replace(elem.name,'')}
            if(this.categories[elem.id].selected ===true){
            this.maininput = this.maininput + ' ' + elem.name;
            }
        },
        PostVid (){
            axios({
                method: 'post',
                url: 'https://lobster.tools/api/v1/categories',
                // url: 'https://lobster.tools/api/v1/projects',
                data: {
                    name: this.maininput,
                    selected: false,
                },
                headers: {
                    "Content-type": "application/json; charset=UTF-8",
                    'Access-Control-Allow-Headers': 'x-requested-with, Content-Type, origin, authorization, accept, x-access-token',
                    'Access-Control-Allow-Origin': '*',
                    'Access-Control-Allow-Methods': 'POST, GET, OPTIONS, DELETE, PUT',
                    'Access-Control-Allow-Max-Age': '1000',
                    'Authorization': 'Bearer BT3HK2NpCnyrKiDo',
                },

            })
                .then(response => {this.categories = response.data})
                .catch(function(error) {
                    console.log(error);
                });
            this.reset();
        }
    },
    computed: {
        SearchFun() {
            return this.categories.filter(item => item.name.indexOf(this.searchvalue) !== -1)
        },
    },
    beforeMount () {
            axios({
                method: 'get',
                url: ' http://localhost:3000/categories:',
                // url: 'https://lobster.tools/api/v1/categories',
                // url: 'https://lobster.tools/api/v1/projects',
                headers: {
                    "Content-type": "application/json; charset=UTF-8",
                    'Access-Control-Allow-Headers': 'x-requested-with, Content-Type, origin, authorization, accept, x-access-token',
                    'Access-Control-Allow-Origin': '*',
                    'Access-Control-Allow-Methods': 'POST, GET, OPTIONS, DELETE, PUT',
                    'Access-Control-Allow-Max-Age': '1000',
                    'Authorization': 'Bearer BT3HK2NpCnyrKiDo',//
                }
            })
                .then(response => {this.categories = response.data})
                .catch(function(error) {
                    console.log(error);
                });
    },
}
</script>
<style>
    .sel {
        display: flex;
        flex-direction: row;
        border: 1px solid;
        color: lightgray;
        border-radius: 2px;
    }
    .search{
        border: 1px solid !important;
    }
    .inp{
        display: flex;
        flex-direction: column;
    }
    .sersel{
        display: flex;
        flex-direction: row;
    }
    .active{
        background-color: red;
        color: white;
    }
    .active2{
        background-color: red;
        color: white;
    }
    form {
        display: flex;
        flex-direction: row;
    }
    input {
        -webkit-appearance: none;
        -moz-appearance: none;
        border: none;
        position: relative;
        outline: none;
        padding: 5px;
        padding-right: 40px;
    }

</style>